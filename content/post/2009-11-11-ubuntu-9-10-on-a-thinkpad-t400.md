---
title: Ubuntu 9.10 on a Thinkpad T400
author: Michael Schurter
layout: post
date: 2009-11-12
url: /2009/11/11/ubuntu-9-10-on-a-thinkpad-t400/
dsq_thread_id:
  - 463870966
categories:
  - GNU/Linux
  - Open Source
  - Technology
tags:
  - ubuntu

---
I upgraded from Ubuntu 9.04 to [9.10][1] on my Lenovo Thinkpad T400 about a week ago, and thought I&#8217;d write down some of my impressions.

**Good news**

  * ATI graphics card with proprietary binary driver &#8211; just works (much better than 9.04 as well).
  * Suspend & hibernate work flawlessly.
  * Boots fast.
  * Upgrade worked flawlessly.
  * Sound (better volume panel!), wifi, USB, network printer, bluetooth (option to turn it on/off!), webcam, etc. all still work.
  * New theme is nice.
  * I manually [upgraded my filesystem to ext4][2] and [grub from version 1 to 2][3]. It was a bit scary but worked out fine. Can&#8217;t really feel a difference, but my laptop is mainly a dumb terminal for running web browsers and ssh. </ul> 
    **[Empathy][4]**
    
    Ubuntu replaced Pidgin with Empathy as the default IM client in Ubuntu 9.10. I think because Empathy supports voice/video chat and Pidgin doesn&#8217;t? I&#8217;ve used video chat once in my life and that was through Skype on Linux. It worked great, but it&#8217;s really not a feature I care about.
    
    So for someone like me who doesn&#8217;t care about Empathy&#8217;s singular advantage over Pidgin, Empathy is a major step backward. At first it was extremely crashy, but a recent update seems to have fixed that. However, now it mysteriously loses messages. I&#8217;m a very light IM user, but it would start silently missing messages a few hours into the day every day.
    
    I&#8217;ve switched back to Pidgin and couldn&#8217;t be happier.
    
    **Message Notification applet deal**
    
    Empathy integrates with the message notification applet deal along with Evolution. Other apps may as well, but evidently I don&#8217;t use any of them. My top panel is 75% whitespace, so the singular benefit of Ubuntu&#8217;s consolidated message notification applet was completely lost on me.
    
    So much like Empathy, I removed this specialized applet as well. I&#8217;m much happier with per-application icons anyway and fail to see what the benefit of consolidating them is (unless you have a really cramped top panel).
    
    **New Theme**
    
    I like it, but then I installed Chromium. Now the bold window titles and expansive title bars in Metacity look bulky and antiquated. Gnome really needs to evolve their window manager and default UI. Chrome is an excellent example of how to design a compact, minimal, yet still pleasant and intuitive user interface.
    
    **[Ubuntu Software Center][5]**
    
    What a curious little replacement for the old Add/Remove Applications program. I think I see the direction they&#8217;re headed, but it definitely feels like rolled out a beta program to replace a perfectly functional and stable one.
    
    The left pane with expansive whitespace and 2 options _hints_ that there might be more categories in the future, but right now it just looks like a mistake. Like maybe something isn&#8217;t working properly, and I&#8217;m not seeing all the options I should see.
    
    At any rate, I hope Ubuntu adds an App Store that even includes evil proprietary software. I&#8217;d love to be able to plunk down a few bucks for a game like [Braid][6] directly from Ubuntu Software Center. That&#8217;d be great! Maybe Canonical could even pocket a few pennies and start making Linux-on-the-desktop profitable. Now I&#8217;m just dreaming though&#8230;
    
    **Bottom Line**
    
    9.10 is a solid and safe upgrade for any users of previous versions. Not sure there&#8217;s anything new to win over users from OS X or Windows though.

 [1]: http://www.ubuntu.com/products/whatisubuntu/910features
 [2]: http://ext4.wiki.kernel.org/index.php/Ext4_Howto#Converting_an_ext3_filesystem_to_ext4
 [3]: https://wiki.ubuntu.com/KernelTeam/Grub2Testing
 [4]: http://live.gnome.org/Empathy
 [5]: https://wiki.ubuntu.com/SoftwareCenter
 [6]: http://braid-game.com/