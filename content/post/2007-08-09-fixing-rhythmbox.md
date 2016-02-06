---
title: Fixing Rhythmbox
author: Michael Schurter
layout: post
date: 2007-08-09
url: /2007/08/09/fixing-rhythmbox/
dsq_thread_id:
  - 535613818
categories:
  - GNU/Linux
  - Open Source
  - Technology
tags:
  - Personal

---
It [didn&#8217;t take long][1] before I found a problem with [Rhythmbox][2].* It couldn&#8217;t figure out the MIME type for half of Blonde Redhead&#8217;s newest album _23_ ([download it from emusic][3]).

The simple fix was: `rm -R ~/.gnome2/rhythmbox`

This deletes your playlists and Rhythmbox&#8217;s database which is kind of annoying, but upon starting Rhythmbox is happily re-indexed all of my music automatically.

This command might work just as well:``

   `rm ~/.gnome2/rhythmbox/rhythmdb.xml`

&#8230;it just removes the database file.

<small>* I&#8217;m using Rhythmbox 0.10.1 on Debian Sid.</small>

 [1]: /blog/2007/08/03/goodbye-banshee-welcome-back-rhythmbox/
 [2]: http://www.gnome.org/projects/rhythmbox/
 [3]: http://www.emusic.com/album/Blonde-Redhead-23-MP3-Download/11016357.html