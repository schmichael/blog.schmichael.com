---
title: Web Server Quandary
author: Michael Schurter
layout: post
date: 2008-12-27
url: /2008/12/27/web-server-quandary/
dsq_thread_id:
  - 463870817
categories:
  - GNU/Linux
  - Open Source
  - PHP
  - Python
  - Technology
tags:
  - apache
  - cherokee
  - lazyweb
  - lighttpd
  - nginx
  - PHP
  - Python

---
[Apache][1] was probably the first Linux application I learned how to configure. However, I&#8217;ve gotten a bit frustrated with it recently&#8230;

**The Problem**

_A memory leak._ Apache is eating up memory so quickly that I need to restart it every couple days or risk my entire server grinding to a halt as it starts swapping wildly. I&#8217;ve poured over log files and `pmap` output, but I still can&#8217;t figure out where the problem lies. Curse you monolithic in-process architecture!

Actually I know what my problem is, I&#8217;m running a mess of modules:

  * `ssl` &#8211; 2 certificates on 2 ports
  * `php5` &#8211; blerg, who doesn&#8217;t have to run this?
  * `suphp` &#8211; I suspect this is my problem, but I can&#8217;t prove it. A client&#8217;s 3rd party web application _requires_ it, but I think its easily replaceable with FastCGI.
  * `wsgi` &#8211; No complaints. Python apps are out-of-process thankfully.
  * `proxy` &#8211; Again no complaints. Can&#8217;t imagine how this module could cause any problems except it does proxy some large (multi-megabyte, not huge) POSTs at times. I can&#8217;t imagine a memory leak could slip into this module without a lot of people noticing.

**Solution A: Apache+FastCGI**

I love the idea of putting each web application in its own process and letting Apache just act as an HTTP router. FastCGI seems to have all the features I need, and I&#8217;m not really worried about the CPU overhead incurred by IPC.

However, there are 2 competing FastCGI modules for Apache, and I have no idea what to choose. Anecdotally the official [mod_fastcgi][2] is buggy and [fastcgi.com is a spam infested wasteland][3]. However, I&#8217;ve found no authoritative source saying: _&#8220;fastcgi is dead, long live [fcgid][4]!&#8221;_ (Lame excuse, I know.)

**Solution B: [Lighttpd][5]**

I know Lighty is the darling of Rails sites, but whenever I stop by its site I&#8217;m greeted with a list of recently fixed [security bugs][6], and now it seems as though [they&#8217;re rewriting the core][7]!

I&#8217;m sure Lighty is a high quality intelligently engineered project, but it seems to be the definition of immature. Not necessarily bad (in fact it usually means its progressing quickly!), but perhaps not as reliable as good old workhorses like Apache.

**Solution C: [Cherokee][8]**

I&#8217;ve been following Cherokee for some time now and running it locally on my workstation. I _love_ the web interface. I&#8217;m usually a very anti-webmin, pro-vim kind of guy, but I&#8217;m sick of editing Apache&#8217;s config files. I do it about once a month and therefore it always takes lots of double-checking the docs. I don&#8217;t know why, but its configuration has just never felt natural to me.

However, the lead Cherokee developer&#8217;s bravado is by the most off-putting aspect of the project. [He mocks modwsgi][9] and posts simplistic benchmarks showing Cherokee to be the fastest web server, but meanwhile Cherokee churns out numerous bug patch releases in-between feature releases and has yet to reach 1.0 status.

It seems like an excellent project technically, but I&#8217;m afraid there will be negative consequences for the lead developers hubris. <small>(I&#8217;m not meaning to insult the guy. He&#8217;s probably a far better hacker than I&#8217;ll ever be. Self-promotion just makes me uncomfortable.)</small>

**Solution D: [nginx][10]**

I don&#8217;t know much about nginx except that it works. Basically all I&#8217;ve heard about it is:

  * It works.
  * Its fast. _Really_ fast.

While &#8220;working&#8221; is definitely my primary objective, nginx seems a bit bare bones for me. I just don&#8217;t think I&#8217;m the target demographic. I&#8217;d kind of like for my web server to handle spawning and kill of FastCGI processes.

nginx feels like git to me. Those who know it: use it and love it. Those who don&#8217;t: stand in fear and awe of its unbridled power.

&#8230;or maybe its just a nice simple barebones HTTP server&#8230;

**Conclusions?**

I think **Solution A: FastCGI** is the most sensible. Apache has always served me well, and the memory leak is most likely due to that shoddy suphp module.

Moving my web applications to FastCGI is also the best way to prepare to move to one of these 2nd generation web servers.

However, I&#8217;m getting kind of sick of Apache, and the ambiguousness of which FastCGI solution to choose is fairly annoying.

So dear lazyweb, for your everyday web developer consultant looking to run a bunch of PHP and Python web applications, what HTTP server stack should I use? (Debian Lenny packages are a plus.)

 [1]: http://httpd.apache.org/
 [2]: http://www.fastcgi.com/drupal/node/3
 [3]: http://www.fastcgi.com/drupal/node/2
 [4]: http://fastcgi.coremail.cn/
 [5]: http://www.lighttpd.net/
 [6]: http://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=lighttpd
 [7]: http://blog.lighttpd.net/articles/2008/12/02/a-little-heads-up
 [8]: http://www.cherokee-project.com/
 [9]: http://lists.octality.com/pipermail/cherokee/2008-December/009437.html
 [10]: http://nginx.net/