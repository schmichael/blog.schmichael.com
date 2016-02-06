---
title: aoss to the rescue
author: Michael Schurter
layout: post
date: 2005-10-07
url: /2005/10/07/aoss-to-the-rescue/
dsq_thread_id:
  - 535533807
categories:
  - Open Source
tags:
  - Personal

---
So in less time than it took me to [post about my problems with RealAudio in Debian yesterday][1] I fixed it today. The `alsa-oss` package contains a handy little tool called `aoss`.

To run an application built for OSS on a computer using ALSA just type:
  
`aoss app-name`
  
in a Run dialog or terminal window.

I created a shortcut to RealPlayer on my wife&#8217;s top panel and prepended `aoss` to the command line for it.

If RealPlayer was an official Debian package I might file a bug saying it ought to depend on (or suggest) OSS or alsa-oss.

 [1]: http://blogs.synthesyssolutions.com/michael/2005/10/07/real-audio-in-debian/