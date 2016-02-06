---
title: MmStats in Scripts
author: Michael Schurter
layout: post
date: 2012-10-03
url: /2012/10/03/mmstats-in-scripts/
dsq_thread_id:
  - 869199655
categories:
  - Python
tags:
  - mmstats
  - Python

---
[MmStats][1] is a library I created to expose and read statistics, metrics, and debugging information from running Python processes without the overhead of syscalls (eg writing to a socket or file) or threads, and to make sure that as many utilities as you want can read those metrics without affecting the performance of the main process exposing stats.

I [released 0.7][2] today to ease integration into multithreaded apps, but it made me realize a simpler tutorial would probably be helpful.

While I had web apps, job consumers, and other long running daemons in mind when I wrote mmstats, it turns out it&#8217;s also excellent for long running scripts.

You know the scripts: maintenance scripts, &#8220;fixer&#8221; scripts, slow build or deployment scripts, data migration scripts, etc.

If you&#8217;re like me, you always forget 2 things every time you write and run one of these scripts:

  1. Run it in `screen`
  2. Periodic progress output

Luckily for #1 there&#8217;s already [disown][3].

For #2 we need an example script. Let&#8217;s pretend you have a Django app with users and you need to update their email addresses in a different system with something like this:

<pre lang="python">import otherdb
from django.contrib.auth import models

for user in models.User.objects.all():
    otherdb.update(user.username, email=user.email)
</pre>

After forgetting to run it in screen, I&#8217;d restart it &#8230; and sit there &#8230; staring at my terminal &#8230; hating myself for not having it output anything.

But then these scripts never work the first time, so it&#8217;d probably die in flames on the first user without an email or similar exceptional condition I forgot to take into account.

So on my second attempt I&#8217;d probably quickly try to cobble together some progress indicator:

<pre lang="python">import otherdb
from django.contrib.auth import models

BATCH = ...

for i, user in enumerate(models.User.objects.all()):
    if i % BATCH == 0:
        print '{0} done'.format(i)

    # Only update users who have emails! Otherwise otherdb dies.
    if user.email:
        otherdb.update(user.username, email=user.email)
</pre>

But what should `BATCH` be? If I have 10,000 users, `BATCH = 1000` seems reasonable, but what if `otherdb` is _really_ slow? In that case a smaller batch like 100 or 50 might be appropriate, so I don&#8217;t have to worry if `otherdb` just became unresponsive or something.

The best option is to **always have your precise progress available at your request.**

# Using MmStats in Scripts

I&#8217;ve found mmstats fits this use case beautifully. No more guessing at what might be an appropriate batch size or using the wrong format string in an uncommon case and crashing my script halfway through.

Integrating mmstats is as easy as:

<pre lang="python">import time
import mmstats
import otherdb
from django.contrib.auth import models

# Define your stats in a model
class S(mmstats.MmStats):
    done = mmstats.CounterField(label="done")
    missing_email = mmstats.CounterField(label="missing_email")
    otherdb_timer = mmstats.TimerField(label="otherdb_timer")
    last_user = mmstats.StringField(label="user")

# Instantiate the stats model
stats = S(filename="update-emails-{0}.mmstats".format(time.time()), path=".")

for i, user in enumerate(models.User.objects.all()):
    # Update the username for readers to see
    stats.last_user = user.username

    # Only update users who have emails! Otherwise otherdb dies.
    if user.email:
        with stats.otherdb_timer:
            # Actually do the migration work
            otherdb.update(user.username, email=user.email)
    else:
        stats.missing_email.inc()

    # Increment the done counter to show another user has been processed
    stats.done.inc()
</pre>

That&#8217;s it! Now just re-run in screen, pop back into a shell and check on the progress with `slurpstats`:

<pre lang="bash">schmichael@prod9000:~$ slurpstats *.mmstats
==> ./update-emails-1234567890.mmstats
  done               113
  missing_email      12
  otherdb_timer      0.3601293582
  user               rob
  sys.created        1346884490.7
  sys.pid            10298
  sys.gid            549
  ...
</pre>

This output would indicate 113 users have been checked, 12 of them had no email, &#8220;rob&#8221; is the current user being processed, and that `otherdb.update(...)` takes on average 360ms to complete. <small>By default timers average the last 100 values, but that&#8217;s customizable via the size keyword argument.</small>

That&#8217;s nice and all, but it&#8217;d be more fun to see **how many users were updated per second.** `pollstats` is a simple tool for doing just that:

<pre lang="bash">schmichael@prod9000:~$ pollstats done,missing_email *.mmstats
       done         |      missing_email
                213 |                 20
                  3 |                  0
                  5 |                  1
                  1 |                  0
...
</pre>

`pollstats` will print out the current value of the given counters initially, and then once per second print the delta. So in our contrived example we&#8217;d be processing somewhere between 1 and 5 users per second and less than 1 missing email per second.

Sadly `pollstats` is extremely simplistic at the moment and lacks the ability to intelligently display non-counter fields. (Patches welcome!)

Even better: if you&#8217;re script dies the mmstats file will be left for you to inspect. (Although if you want it perfectly in sync you should probably `stats.flush()` on each iteration.)

mmstats is still young (pre-1.0 for a reason) and simplistic, but I already find it extremely useful not only in web apps and other daemons, but also in simple &#8211; or not so simple &#8211; one-off scripts. I hope you find it useful as well!

 [1]: http://mmstats.readthedocs.org/
 [2]: http://pypi.python.org/pypi/mmstats/0.7.0
 [3]: http://playingwithsid.blogspot.com/2007/10/disown-nohup-bash-commands.html