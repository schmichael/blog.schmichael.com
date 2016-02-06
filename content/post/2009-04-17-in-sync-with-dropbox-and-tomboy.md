---
title: Keeping all your notes in sync with Dropbox and Tomboy
author: Michael Schurter
layout: post
date: 2009-04-18
url: /2009/04/17/in-sync-with-dropbox-and-tomboy/
dsq_thread_id:
  - 465637889
categories:
  - GNU/Linux
  - Mono/.Net
  - Open Source
  - Technology
tags:
  - dropbox
  - gnome
  - tomboy

---
[Tomboy][1] is a wonderful note taking program for Gnome. It has some synchronization features built-in, but not everyone has a server to store their notes for synchronizing between multiple computers.

Enter [Dropbox][2]: a service for synchronizing files between computers. It works great in Gnome (Windows and Mac OSX as well).

I use Dropbox for synchronizing my Tomboy notes by telling Tomboy to synchronize to a Local Folder: `~/Dropbox/Tomboy`

My one gripe is that you have to go into a note to synchronize. [Someone has filed a bug and submitted a patch][3], so hopefully it will be fixed soon.

 [1]: http://projects.gnome.org/tomboy/
 [2]: https://www.getdropbox.com/referrals/NTE2ODkwNDk
 [3]: http://bugzilla.gnome.org/show_bug.cgi?id=468459