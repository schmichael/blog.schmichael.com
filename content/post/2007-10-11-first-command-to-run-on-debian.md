---
title: First Command to Run On Debian
author: Michael Schurter
layout: post
date: 2007-10-11
url: /2007/10/11/first-command-to-run-on-debian/
dsq_thread_id:
  - 621948383
categories:
  - GNU/Linux
  - Technology
tags:
  - Lo-Fi Art

---
(Also applies to Ubuntu if you have a SSH server installed.)

<pre lang="bash">sudo apt-get install denyhosts
</pre>

[DenyHosts][1] is a [Python][2] application that monitors [SSH][3] authentication attempts and block hosts with multiple failures. While its configuration file is easy to figure out, the defaults work well for me.

Every SSH server should be running DenyHosts or a similar security application. Running without it is like running Windows without anti-virus.

 [1]: http://denyhosts.sourceforge.net/
 [2]: http://python.org/
 [3]: http://en.wikipedia.org/wiki/Ssh