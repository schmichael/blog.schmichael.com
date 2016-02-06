---
title: WebKit for Gnome
author: Michael Schurter
layout: post
date: 2007-08-26
url: /2007/08/26/webkit-for-gnome/
dsq_thread_id:
  - 469442782
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
<div style="margin: 6px; float: right">
  <a href="http://michael.susens-schurter.com/blog/wp-content/uploads/2007/08/webkit-gdklauncher.png" title="WebKit GdkLauncher"><img src="http://michael.susens-schurter.com/blog/wp-content/uploads/2007/08/webkit-gdklauncher.thumbnail.png" alt="WebKit GdkLauncher" /></a>
</div>

[WebKit for Gnome just landed in Debian&#8217;s unstable repository][1]. Unfortunately its just the libraries for now, but it does include a testing GUI called GdkLauncher.

If you&#8217;re not familiar with [WebKit][2], it is the open source HTML/CSS/JavaScript rendering engine that powers [Apple&#8217;s Safari browser][3]. (WebKit is to Safari as [Gecko is to Firefox][4].)

You can play around with the test browser by running: **`/usr/lib/WebKit/GdkLauncher<code>`</code>**

I&#8217;m excited about having an alternative to Gecko. Its not that I&#8217;m unhappy with Firefox or Epiphany. Its just that selection and choice is always nice. Hopefully WebKit will do some things better than Firefox (like not use tons of memory). For now its mostly a toy.

I browsed around using GdkLauncher for a bit. Google Reader and a number of other pages I tried worked. However, when I tried to login to WordPress to blog, it crashed.

You can [watch WebKit (via GdkLauncher) in action in a **screencast** (_ogg_ format)][5] I made with [RecordMyDesktop][6].

 [1]: http://packages.debian.org/unstable/libs/libwebkitgdk0d
 [2]: http://webkit.org/
 [3]: http://www.apple.com/safari/
 [4]: http://en.wikipedia.org/wiki/Gecko_(layout_engine)
 [5]: http://michael.susens-schurter.com/files/webkit-gdklauncher.ogg
 [6]: http://recordmydesktop.iovar.org/