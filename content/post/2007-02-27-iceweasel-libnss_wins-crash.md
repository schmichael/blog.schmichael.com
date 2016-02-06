---
title: Iceweasel + libnss_wins = Crash
author: Michael Schurter
layout: post
date: 2007-02-27
url: /2007/02/27/iceweasel-libnss_wins-crash/
dsq_thread_id:
  - 463870414
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
I hate the fact that [Firefox][1], probably the most recognizable open source brand name, was hastily renamed [<span style="font-style: italic">Iceweasel</span>][2] in [Debian Etch][3] due to trademark issues.

So I&#8217;ve been especially sensitive lately as Iceweasel seems to be crashing on me all the time. I&#8217;ve uninstalled my add-ons, cleared my cache, and tried to debug the issue.

I finally caught a crash while attached to Iceweasel using [gdb][4]. Looks like libnss_wins ([Samba][5]&#8216;s WINS name lookup service) is to blame:

`Program received signal SIGBUS, Bus error.<br />
[Switching to Thread -1288709200 (LWP 28528)]<br />
0xb1a98309 in toupper_w () from <strong>/lib/libnss_wins.so.2</strong>`

Of course I just failed to duplicate the crash&#8230;

**Update:** Removing wins from my nsswitch.conf works and doesn&#8217;t seem to hurt anything else.

 [1]: http://www.getfirefox.com/
 [2]: http://en.wikipedia.org/wiki/IceWeasel
 [3]: http://www.debian.org/releases/etch/
 [4]: http://sourceware.org/gdb/
 [5]: http://samba.org