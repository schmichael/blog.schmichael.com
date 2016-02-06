---
title: Setting Up Yet Another Debian Etch Server
author: Michael Schurter
layout: post
date: 2007-01-25
url: /2007/01/25/setting-up-yet-another-debian-etch-server/
dsq_thread_id:
  - 547338920
categories:
  - GNU/Linux
  - IT
  - Open Source
  - PHP
  - SQL
  - Technology

---
A teacher e-mailed me the other day wondering if I could setup a server with [Moodle][1] on it for him to test. I was overjoyed at the request because the teacher had discovered Moodle, [MySQL,][2] [PHP,][3] and Linux (as well as their freeness) all by himself!

I used the [Debian][4] [Etch][5] [Net Install Daily Image][6] for today (1/25/2007), and everything went pretty smoothly.

**Installation**

I thought I had entered &#8220;installgui&#8221; at the boot prompt, but I still got the old text based setup. Everything went smoothly, so I have no complaints. Perhaps the net installation doesn&#8217;t have the GUI installer?

One scary thing did happen during installation: after the initial reboot Linux ran fsck on the new installation and found a number of errors! After another reboot everything appears to be working normally. This is an old PIII computer, so I&#8217;m immediately installing smartmontools.

**Setup**

GDM came up with a few colored vertical lines. One [Google search later][7] [I discovered that the i810 Intel driver might do that at higher resolutions][8]. I lowered my resolution to 1024 x 768 and everything works beautifully.

Upon updating my package lists in Synaptic, I got some strange errors from gpg, so Debian can&#8217;t validate a number of packages. A bit strange, but it doesn&#8217;t hurt anything.

**apt-zeroconf**

Thanks to [apt-zeroconf][9] I downloaded the 40+ megs of extra packages I needed mostly off of my other 2 local Debian boxes. Now if only I could configure the net install CD to use apt-zeroconf&#8230; hm&#8230; Sounds like a job for lazyweb!

I do get periodic 404 errors when using apt-zeroconf, but just trying again fixes it every time.

**Summary**

All things considered I didn&#8217;t see any reason not to **release Etch immediately**!

_I still recommend [Ubuntu][10] or [openSUSE][11] for normal users or people new to Linux as Debian just doesn&#8217;t do enough hand holding for people not willing to spend some time learning Linux._

 [1]: http://moodle.org/
 [2]: http://mysql.com/
 [3]: http://php.net/
 [4]: http://www.debian.org/
 [5]: http://www.debian.org/releases/etch/
 [6]: http://cdimage.debian.org/cdimage/daily-builds/daily/arch-latest/i386/iso-cd/debian-testing-i386-netinst.iso
 [7]: http://michael.susens-schurter.com/blog/xorg%20intel%2082815
 [8]: http://www.linuxquestions.org/hcl/showproduct.php/product/2851
 [9]: http://trac.phidev.org/trac/wiki/AptZeroconf
 [10]: http://www.ubuntu.com/
 [11]: http://www.opensuse.org/