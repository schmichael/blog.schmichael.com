---
title: History Meme
author: Michael Schurter
layout: post
date: 2008-04-11
url: /2008/04/11/history-meme/
dsq_thread_id:
  - 463870714
categories:
  - GNU/Linux
  - Open Source
  - Python
  - Technology
tags:
  - ipython

---
For some reason I find this meme interesting&#8230; I don&#8217;t know why I find it interesting, but at least its brief.

**Home Office Computer** (Debian Unstable)

<pre lang="bash">$ history|awk '{a[$2]++} END{for(i in a){printf "%5d\t%s\n",a[i],i}}'|sort -rn|head
   99	sudo
   80	cd
   59	ssh
   52	vi
   47	ls
   19	cat
   17	ipython2.5
   12	svn
   12	man
    8	host</pre>

**Server I do most of my work on these days&#8230;** (Ubuntu 6.10)

<pre lang="bash">$ history|awk '{a[$2]++} END{for(i in a){printf "%5d\t%s\n",a[i],i}}'|sort -rn|head
  288	vi
  108	svn
   59	cd
   15	ls
    8	screen
    4	grep
    2	sudo
    2	mv
    2	make
    2	cat</pre>

I haven&#8217;t seen `ipython` on anyone else&#8217;s yet. I&#8217;m constantly hopping in & out of ipython to test things.

On the GUI side of things I use Gnome, Firefox, Epiphany, Gnome-Terminal, Banshee, Pidgin, and NetworkManager every day.