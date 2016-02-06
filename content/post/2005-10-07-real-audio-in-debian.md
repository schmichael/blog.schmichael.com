---
title: Real Audio in Debian
author: Michael Schurter
layout: post
date: 2005-10-07
url: /2005/10/07/real-audio-in-debian/
dsq_thread_id:
  - 463869844
categories:
  - GNU/Linux
  - Open Source
tags:
  - Personal

---
While my wife Samantha is usually quite content with our home computer running [Debian GNU/Linux][1] ([Etch][2]), she does have a few quite valid gripes.

The big one as of late has been the poor state of audio support in Linux. Sam and I both love [NPR][3], and in particular the show [This American Life][4]. Unfortunately This American Life only provides shows online in the [proprietary Real Audio][5] format (unless you want to shell out cash for some DRM&#8217;d MP3s).

As far as I can tell, RealPlayer (and Helix) for Linux only support OSS based audio. My computer uses [ALSA][6], and I had to fight to get that to work!

It&#8217;s frustrating that something as ubiquitous as audio is so tough to configure in Linux. First there&#8217;s OSS and ALSA at the kernel level. Then there&#8217;s a number of userspace daemons and libraries which wrap kernel level audio. However, some applications access OSS or ALSA directly, some use daemons, some use libraries, and some use a pluggable backend which as far as I can tell just means none-of-the-above work without hacking. (And some apps use libraries which use pluggable backends&#8230;)

Hopefully I can post again in the next few days with a solution.

 [1]: http://www.debian.org/
 [2]: http://www.us.debian.org/releases/etch/
 [3]: http://www.npr.org
 [4]: http://www.thislife.org/
 [5]: http://www.realaudio.com/
 [6]: http://www.alsa-project.org/