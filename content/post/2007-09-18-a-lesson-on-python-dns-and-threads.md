---
title: A Lesson on Python, DNS, and Threads
author: Michael Schurter
layout: post
date: 2007-09-18
url: /2007/09/18/a-lesson-on-python-dns-and-threads/
dsq_thread_id:
  - 463870556
categories:
  - Open Source
  - Python
  - Technology

---
While working on a firewall project <small>(that I&#8217;ll hopefully be posting about soon)</small>, I ran across the need to resolve thousands of domain names to IP addresses as quickly as possible (without duplicates). It was a simple, straightforward problem which proved to be a great learning experience!

To follow along at home you&#8217;ll need to download <strike>proxies.txt</strike> and put it in the same directory as the Python scripts below. **Update: I removed the proxiest.txt file&#8230; too many hits for all the wrong reasons I&#8217;m sure.**

<strike>Spoiler</strike> _Obvious Warning: If you need to do lots of DNS queries, **don&#8217;t reinvent the wheel: use an asynchronous DNS library**. These examples are useful for people interested in learning about threading and optimizing simple tasks._

**First Try: Synchronous DNS Lookups**

Always try the simplest solution first: loop over the list of domain names and add each resolved IP to a set. A set is by definition a unique list, so it won&#8217;t contain duplicate IP entires.

The Python code is short enough to post here, but WordPress really likes messing with my whitespace, so [I uploaded it to pastebin][1].

Unfortunately doing synchronous DNS lookups on 3,000 domain names took about **2 hours** on my machine!

_Bottom line:_ 2 hours is not acceptable.

**Second Try: [Threads][2] and [Semaphores][3]**

I know threads are overkill, but it just wouldn&#8217;t be fun if I went straight to using asynchronous DNS. 😉 I also wanted to try using threads on Python which in general have a bad reputation due to the GIL.
  
[
  
Download try2.py][4] and execute it with &#8220;`time python try2.py`&#8221; to see how long it takes to do the lookups. It took **40 seconds** on my computer.

However, if you set &#8220;`easyadns_debug = False`&#8221; in the code, suddenly I get a &#8220;`thread.error: can't start new thread`&#8221; exception. I believe this is because the code is starting about 3,000 new threads in a tight loop which isn&#8217;t a very nice thing to do.

I use a counting semaphore with a value of 50 to ensure only 50 lookups are performed at a time, but this doesn&#8217;t stop the script from spawning 3,000 threads immediately! I&#8217;m guessing all of the `print` statements that occur when easyadns_debug is true slow down the process just enough to allow Python to sanely handle all of the new threads.

_Bottom line:_ 40 seconds is good, but causing difficult to debug exceptions is unacceptable.

**Third Try: Thread Pool**

At this point I should have bitten the bullet and sought out a _real_ asynchronous DNS library, but I had to at least try threads properly before giving up on them.

[Download try3.py][5] and execute it with &#8220;`time python try3.py`&#8220;.

Just like with try2.py you can set easyadns_debug to False to disable all of the output, but unlike try2.py, this version won&#8217;t crash if you do!

My third try uses a thread pool to handle the lookups. 50 threads are created and pop domain names off of the master list. This method requires a lock on both the input and output data variables which adds overhead.

With debugging on the script takes **3 minutes 20 seconds** to do the lookups, and disabling debugging output seems to save about 20 seconds.

_Bottom Line:_ 3 minutes isn&#8217;t bad, but from the 2nd try we know there&#8217;s a more efficient way.

**Solution: [adns-python][6]**

adns-python&#8217;s nearly complete lack of documentation scared me away at first, but with a little toying around in ipython its pretty straightforward. Its just a &#8220;sudo apt-get install python-adns&#8221; away in Debian Sid.

[Download try4.py][7] and execute it with &#8220;`time python try4.py`&#8220;.

As always you can turn off debugging messages easily. However, even with debugging on this script completes in a little over **20 seconds**.

Using a callback instead of the while loop starting on line 15 would be preferable, but I didn&#8217;t see how to use callbacks in the version of adns-python I was using. Callbacks would also introduce the need to lock `data` before adding IPs to it.

_Bottom line:_ No threads. No locks. Less code. Good performance. We have a winner!

Some random things I learned while doing all of this:

  * The bottleneck for DNS lookups is the **timeout**. Failed lookups will wait multiple seconds before timing out while successful DNS queries will return results in a fraction of a second.
  * Python threading is _not_ worthless because of the GIL. It will be interesting to see where experiments in Python concurrency lead, but I don&#8217;t see the GIL as a limiting factor for Python.
  * Because of the GIL I may not have need to lock around my variables. This could have improved performance, but I wanted to write the code using the correct principles. I would hope you could port these examples to another language and get similar results.
  * It&#8217;s hell to post code in WordPress. I thought installing a code formatting plugin would help, but it doesn&#8217;t seem to stop WordPress from mangling my whitespace randomly.

**Aug 1st, 2010 &#8211; Update:** Disabled comments on this post as it seems to attract a disproportionate amount of spam.

 [1]: http://python.pastebin.com/f4292b7fa
 [2]: http://docs.python.org/lib/module-threading.html
 [3]: http://en.wikipedia.org/wiki/Semaphore_(programming)
 [4]: /code/easyadns/try2.py
 [5]: /code/easyadns/try3.py
 [6]: http://code.google.com/p/adns-python/
 [7]: /code/easyadns/try4.py