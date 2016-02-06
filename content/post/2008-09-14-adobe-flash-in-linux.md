---
title: Adobe Flash in Linux
author: Michael Schurter
layout: post
date: 2008-09-14
url: /2008/09/14/adobe-flash-in-linux/
dsq_thread_id:
  - 677236602
categories:
  - GNU/Linux
  - Technology
tags:
  - debian
  - flash
  - gnash
  - GNU/Linux
  - swfdec

---
Like most people, I use Flash a lot. Not only do I watch YouTube and Hulu videos, but FusionCharts* are an integral part of one of the main projects I work on. And like most people, I just want Flash to work. While an open source option would be nice, I really just need something that works.

Unfortunately **Flash in Linux** <small>still</small> **sucks.**

Fortunately, **not for long.**

**Flash 9**

For a long time I&#8217;ve just used the [flashplugin-nonfree][1] (such an attractive package name) package to get Flash support.

In general this works great, unless you want to also use [PulseAudio][2]. For some reason I do, which means my audio is always out of sync. Apparently Ubuntu has a flashplugin-nonfree-pulse (another awesome package name), but [Debian won&#8217;t package it because of issues with upstream, and the fact the upcoming Flash 10 works fine without any extra wrappers][3].

**Flash 10**

So I finally decide to just try out the betas of [Flash 10][4]. At this point in time, Flash 10 beta 2, is the latest, so I download it and copy the `.so` file to `/usr/lib/mozilla/plugins/`.

Tada! Sync&#8217;d audio! Yay!

Except now my browser crashes on about 1 out of every 2 sites with Flash. Some Flash doesn&#8217;t render completely. Other Flash videos flicker horribly.

Bottom line is even Ubuntu&#8217;s notoriously unstable alpha&#8217;s are better than trying to use Flash 10 beta 2.

**Update:** Just tried Flash 10 RC 1, but its not better than beta 2. Actually it might be a bit better because it crashes _less_, but its more frustrating in other ways: _some Flash videos don&#8217;t show up at all._

**swfdec**

One last thing to try: [swfdec][5], an open source Flash player. I&#8217;ve followed its development closely on Planet Gnome and really respect its developer, [Benjamin Otte][6]. Unfortunately it makes Flash 10 beta 2 look good by comparison. To be fair I used the unstable 0.7.4 version of swfdec, so maybe thats why it crashes fairly often. 0.8 was just released, but evidently not packaged for Debian yet.

I&#8217;ll probably keep trying swfdec from time to time in the future as I _want_ to use it, but for now I just need a Flash player that works.

**[Gnash][7]**

I should try it, but the FSF can be such dicks I have a hard time even wanting to try it. They have a stupid &#8220;Bad Vista&#8221; logo in the upper right corner of their home page. I&#8217;m no fan of Vista, but plastering the Internet with poorly drawn negative logos isn&#8217;t going to win friends.

I shouldn&#8217;t let politics affect whats essentially a purely pragmatic endeavor**, so I&#8217;ll probably end up trying it out.

**Conclusion**

I can&#8217;t wait for Flash 10 to be released. While I love open source, Adobe makes excellent products, and I just need Flash to work. Its like my graphics driver: I really don&#8217;t care about the source, just make my graphics work!

<small>* Very pretty product. Decent documentation. Worthless JavaScript API and debugging features. I hope <canvas> becomes a viable alternative soon.</small>

<small>** That endeavor being: get Flash to work as well in Linux as it does in Windows.</small>

 [1]: http://packages.debian.org/sid/flashplugin-nonfree
 [2]: http://pulseaudio.org/
 [3]: http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=477266#35
 [4]: http://labs.adobe.com/downloads/flashplayer10.html
 [5]: http://swfdec.freedesktop.org/wiki/
 [6]: http://blogs.gnome.org/otte/
 [7]: http://www.gnu.org/software/gnash/