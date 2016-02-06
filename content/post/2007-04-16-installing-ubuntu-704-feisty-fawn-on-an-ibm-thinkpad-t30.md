---
title: Installing Ubuntu 7.04 “Feisty Fawn” on an IBM ThinkPad T30
author: Michael Schurter
layout: post
date: 2007-04-16
url: /2007/04/16/installing-ubuntu-704-feisty-fawn-on-an-ibm-thinkpad-t30/
dsq_thread_id:
  - 463870454
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
Even though I&#8217;m a Debian user, I usually recommend Ubuntu to most people looking for a Linux desktop distribution. I recently got handed an IBM ThinkPad T30 that was donated to my school, so I thought it was about time I took my own advice and install Ubuntu.

I booted [Ubuntu][1] [7.04 &#8220;Feisty Fawn&#8221;][2]. While the Prism 2.5 based WiFi adapter didn&#8217;t &#8220;Just Work&#8221;, Ubuntu appears to detect it properly, and some quick Googling reveals that it should work with a little fiddling.

I start the Install application, and I&#8217;m reminded how slow LiveCDs are on systems with less than 1 GB of memory. While sluggish, the Install app is very easy to use. It detected my Windows XP partition and offered to _import my bookmarks, documents, etc._ Very impressive!

The installer froze at 15% for a long time, but after a while it completed the installation without a problem.

Feisty Fawn is pretty bleeding edge: Gnome 2.18, OpenOffice.org 2.2, Python 2.5, etc.

The best part, running **compiz &#8211;replace &** in Gnome terminal gave me all the fancy Compiz effects. No fiddling with xorg.conf. No confusing installation procedures for proprietary drivers. **It just worked.**

I&#8217;m very impressed and will probably keep using Ubuntu instead of Debian for workstations.

**Update:** It looks like my WiFi card has been bitten by [this regression][3].

**Update 2:**Â  Its worth noting that my WiFi card didn&#8217;t work with Windows XP SP2 either without proprietary drivers.

 [1]: http://www.ubuntu.com/
 [2]: http://releases.ubuntu.com/feisty/
 [3]: https://bugs.launchpad.net/ubuntu/+source/linux-source-2.6.17/+bug/63989