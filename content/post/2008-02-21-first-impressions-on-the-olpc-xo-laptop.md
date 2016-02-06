---
title: First Impressions on the OLPC XO Laptop
author: Michael Schurter
layout: post
date: 2008-02-21
url: /2008/02/21/first-impressions-on-the-olpc-xo-laptop/
dsq_thread_id:
  - 482400861
categories:
  - GNU/Linux
  - Open Source
  - Python
  - Technology
tags:
  - olpc
  - xo

---
Last night [Dennis Gilmore, Build Engineer][1] for [OLPC][2], spoke at [Bradley University][3]. Since I live 3 blocks from Bradley and have been following OLPC off and on since the beginning, I couldn&#8217;t pass this up (even though I was the token old guy in a classroom mostly full of college undergrads).

Dennis had brought 3 XOs with him for the students to play with. He gave a good introductory presentation on OLPC, XO, and Sugar. Not much new for anyone who has been following the project, but I did learn that the XO runs each activity&#8217;s process in a different uid/gid. The students asked lots of good questions and were obviously excited about OLPC.

Read on if you care to hear my personal experience with an XO&#8230; <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />
  
<!--more-->

<div style="float: right;">
  <img src="/files/xo.jpg" alt="An OLPC XO Laptop" />
</div>

**First Impressions of the XO & Sugar**

I played with a Spanish language XO for a bit. They&#8217;re beautiful little machines and smaller than I expected. While the plastic that made up most of the case felt like a cheap plastic toy, the overall machine felt very solid. The pop-up antennas were surprisingly strong. I think they just always looked fragile to me in photos.

The rubberized keyboard felt nearly indestructible, but I found it fairly hard to type on. If you don&#8217;t push the keys straight on, its easy to just mash a bit of rubber without actually making a keystroke.

The Sugar interface and activities were very cool if a bit sluggish. Everything I tried _Just Worked_ including networked activities between the XOs. Since I was using a Spanish language version, I quickly came to appreciate how useful Sugar&#8217;s extensive use of iconography is.

**Pippy!**

After poking at a few apps, I quickly made my way to Pippy, the integrated Python development environment. Its pre-populated with fun little example programs and I was playing with the built-in camera and generating sound effects in 30 seconds.

However, Pippy isn&#8217;t an interactive python interpreter, so I quickly switched to ipython to explore further. Unfortunately Pippy invisibly manipulates sys.path, so it took me a bit to get the Pippy example scripts working in ipython.

Once I got the sys.path worked out, programming on the XO was a joy. I quickly had my XO playing off-key chords and could easily poke around the vast number of included python libraries.

**The Good**

The XO seems like an amazing educational tool. It is not a general purpose sub-laptop like the EeePC. Anyone hoping to get one to look cool at the local Starbucks is going to be sorely disappointed. Everything about it seems to be engineered with kids and education in mind, and there&#8217;s no doubt in my mind that it will be a revolutionary educational tool.

**The Bad**

One concern I had was that Python is by-design an English programming language. I&#8217;m not so worried about function and library names as I am about docstrings. I wonder if OLPC has any plans to translate docstrings.

Without translated documentation, I don&#8217;t know how OLPC expects Pippy to be useful outside of English speaking countries. Expecting children to learn English as well as programming seems a bit presumptuous to me.

**The Ugly**

Its been said before, but I&#8217;ll say it again: the XO is sluggish. Applications load slowly and animations aren&#8217;t smooth. The good news is that children may not even notice, but I hope the situation can be improved through software optimization so the current generation of XOs aren&#8217;t banished to sub-standard performance forever.

**Ok, one more good&#8230;**

I&#8217;m more excited about the OLPC project than ever before and hope to meet up with Dennis Gilmore in the future! I&#8217;ll have to post again once I get Sugar running in Qemu.

 [1]: http://ausil.us/blog
 [2]: http://laptop.org/
 [3]: http://www.bradley.edu