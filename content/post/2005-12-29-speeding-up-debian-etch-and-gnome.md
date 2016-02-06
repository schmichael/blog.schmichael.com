---
title: Speeding up Debian Etch and Gnome
author: Michael Schurter
layout: post
date: 2005-12-29
url: /2005/12/29/speeding-up-debian-etch-and-gnome/
dsq_thread_id:
  - 646823160
categories:
  - GNU/Linux
  - Open Source
tags:
  - Personal

---
Over my holiday vacation I ran into some weird crashes while in [Gnome][1] on my [Debian Etch][2] box. Since I don&#8217;t know enough about the internals of Gnome to do any serious debugging, I took the cowards way out and **deleted nearly every dot-file and dot-folder (where settings are kept) in my home directory**.

I kept e-mail, favorites, and the like, but everything else went. I was shocked to find that not only did it **fix the crashes I was experiencing, but Gnome seems to run at least twice as fast as before**.

It only took me about 10 minutes to reset all of the preferences I care about, so my advice to anyone who&#8217;s beeing using Gnome for a while and experiencing crashes, unresponsiveness, or slowdowns: **nuke 90% of the files and folders in your home directory that begin with a dot**.

_**Warning: Be smart, and back everything up first!**_

 [1]: http://www.gnome.org/
 [2]: http://www.us.debian.org/releases/etch/