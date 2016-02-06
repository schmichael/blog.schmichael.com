---
title: 'New Laptop: Acer Extensa 4630Z'
author: Michael Schurter
layout: post
date: 2009-03-23
url: /2009/03/22/new-laptop-acer-extensa-4630z/
dsq_thread_id:
  - 463870878
categories:
  - GNU/Linux
  - Technology
tags:
  - acer
  - ralink
  - ubuntu
  - wifi

---
I bought a laptop recently because being a web consultant and tied to a desktop is not only embarrassing, but is a quick way to lose (or at least frustrate) clients who&#8217;d love to see my hairy hacker face on-site.

I use Linux, Firefox, and vim for work so my requirements for a laptop basically came down to WiFi. I also didn&#8217;t want something big and clunky because I&#8217;m looking to augment my desktop, not replace it.

I finally settled on searching in the 13&#8243;-14&#8243; range for anything with dual cores (so Flash can destroy 1 core while the other lets me continue to work unphased) and 2 GB of RAM (that usually gives me > 1 GB for harddrive caching which speeds things up a lot &#8212; plenty of room to run an XP VM as well).

Despite affectionately nicknaming my aging Thinkpad a &#8220;Brickpad&#8221; due to its big-black-box design, I love Thinkpads and have found them to be exceptionally well made and reliable. Unfortunately they just weren&#8217;t in the budget this around around.

At this point my search had narrowed down a bit, and I began searching for the easiest way to get the most bang for my buck: getting a laptop without Microsoft Windows. Even if Windows only adds $50 to the purchase price, that&#8217;s a significant amount of money when you&#8217;re shopping in the $500-600 range. That and I can remote into the XP VM on my desktop for cross-browser testing (my only use for Windows).

Unfortunately with the exception of tiny netbooks, there aren&#8217;t many Windowless laptops out there (not paying extra for an Apple either, sorry). Dell has one (or a few?), but I&#8217;ve had too many bad experiences with Dells dying prematurely (IMHO, YMMV, etc). HP lets you get Windowless laptops, but only if you pay extra to customize your laptop. Oh well.

So once I gave up on that dream, I just went for cheap and found an [Acer Extensa 4630Z][1].

**Linux on an Acer Extensa 4630Z**

I decided to go with Ubuntu 8.10 instead of my usual choice of Debian and fought around with getting /home and my swap partition encrypted. I&#8217;ll probably keep using Debian on servers, but its politics have just gotten so annoying as to convince me I never really want to work to become a member of that community.

Here&#8217;s the rundown of what works, what doesn&#8217;t:

  * Ralink RT2860 802.11b/g/Draft-N WiFi adapter &#8211; Ugh. Its &#8220;working&#8221; using [Ralink&#8217;s drivers][2], but not with Network Manager. I&#8217;ll have to keep playing around with it, but for now its working adequately.
  * Crazy &euro; and $ keys above the arrow keys do _not_ work, but I&#8217;m not sure what purpose they serve.
  * Intel graphics card works fine with Compiz (although I just use Metacity).
  * Suspend but _not_ hibernate. Argh! Does hibernate work for any Linux users? I haven&#8217;t even tried in years.
  * Webcam, speakers, mic, & screen dimming work

It will interesting to see how I like moving from a Debian desktop to an Ubuntu laptop.

 [1]: http://us.acer.com/acer/productv.do?link=oln15e.redirect&changedAlts=&CRC=1511809838
 [2]: http://www.ralinktech.com/ralink/Home/Support/Linux.html