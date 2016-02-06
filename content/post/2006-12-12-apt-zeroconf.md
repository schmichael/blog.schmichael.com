---
title: apt-zeroconf
author: Michael Schurter
layout: post
date: 2006-12-12
url: /2006/12/12/apt-zeroconf/
dsq_thread_id:
  - 463870275
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
[apt-zeroconf][1] is a fantastic little program that uses [Avahi][2] to automatically find and download packages from other [Debian][3] computers on your LAN with apt-zeroconf installed.

The [configuration][4] is ridiculously easy (I use _Proxy Mode_), and I&#8217;ve already noticed a huge speed increase when updating/installing packages on multiple machines. (Obviously this is only useful for networks with multiple Debian boxes.)

For added fun, you can see how many computers are using apt-zeroconf on your network by installing and configuring [service-discovery-applet][5]:

  1. Install service-discovery-applet with your favorite package manager
  2. Add it to your Gnome panel (you _are_ using Gnome, right?)
  3. Go to Applications > System Tools > Configuration Editor
  4. Open /apps/service-discovery-applet/services
  5. Add a new boolean key called _\_apt.\_tcp_ and set it to true

I always like to see what Avahi/Zeroconf services I&#8217;m publishing, which you can do by right-clicking on the _service-discovery-applet panel icon_, selecting _Preferences,_ going to the _Advanced_ tab, and checking the _Browse services published on this machine_ checkbox.

 [1]: http://trac.phidev.info/trac/wiki/AptZeroconf
 [2]: http://avahi.org/
 [3]: http://www.debian.org/
 [4]: http://trac.phidev.org/trac/wiki/AptZeroconf#Configuration
 [5]: http://packages.qa.debian.org/s/service-discovery-applet.html