---
title: Installing fglrx (ATI) drivers in Debian Etch
author: Michael Schurter
layout: post
date: 2006-11-20
url: /2006/11/20/installing-fglrx-ati-drivers-in-debian-etch/
dsq_thread_id:
  - 463870253
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
The instructions in **/usr/share/doc/fglrx-kernel-src/README.Debian.gz** left something to be desired, so here&#8217;s how I installed the official **ATI display drivers** (_fglrx_) in [Debian Etch][1] (_without rebooting!_):

Here are the relevant packages I have installed. This list may not be exactly what you need but should work. Install using _Synaptic_ or _apt-get_ or what-ever-you-want.

  * fglrx-control, fglrx-driver, fglrx-kernel-src &#8211; 8.28.8-3
  * module-assistant &#8211; 0.10.7
  * mesa-utils &#8211; 6.3.2-2.1 (for the _glxinfo_ command)

Just for reference, here&#8217;s some of my system information:

  * Dell Optiplex GX620
  * ATI RV380 [Radeon X600 (PCI-E)]
  * Debian 4.0 aka Etch (&#8220;testing&#8221; release as of this post)
  * Kernel package: linux-image-2.6.17.2-686 &#8211; 2.6.17-9
  * Gnome 2.14 (important because I use _gdm_ while KDE users probably use _kdm_)

As root run the following:

  1. cd /usr/src
  2. module-assistant prepare
  3. module-assistant a-i fglrx
  4. _Edit your_ /etc/X11/xorg.conf _file, and set your display driver to_ **fglrx** _(it is probably currently set to_ **radeon**_, if not, step #7 will probably be different for you)
  
_ 
  5. _Exit Gnome (or KDE, just get out of X Windows), press ctrl-alt-F1 to get a console, login as root.
  
_ 
  6. /etc/init.d/gdm stop
  7. modprobe -r radeon
  8. modprobe fglrx
  9. /etc/init.d/gdm start
 10. _**Done!**_

To verify that it is installed correctly go to _Desktop_ > _Administration_ > _ATI Control Panel_ and make sure the Renderer is something like _RADEON X600 Pro Generic_. Also run the excellent **glxinfo** tool and make sure it contains the line &#8220;direct rendering: Yes&#8221;.

Many thanks to [dcarvil at forums.debian.net whose post helped me figure out step #7][2].

**Update:** This configuration **does not seem to work with the Composite X.org extension** needed to use _**AIGLX/Compiz**_.Â  AIGLX/Compiz is so new, and there are so many conflicting web sites on how to get it working, that I probably won&#8217;t try to fix this error for a while.

 [1]: http://www.us.debian.org/releases/etch/
 [2]: http://forums.debian.net/viewtopic.php?t=9945&sid=bbb26d5e9c78579e107f9367998d5234