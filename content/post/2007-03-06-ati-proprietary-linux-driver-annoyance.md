---
title: ATI Proprietary Linux Driver Annoyance
author: Michael Schurter
layout: post
date: 2007-03-06
url: /2007/03/06/ati-proprietary-linux-driver-annoyance/
dsq_thread_id:
  - 470370692
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
If you use dual monitors with an ATI video card and [Gnome][1], don&#8217;t use Gnome&#8217;s Screen Resolution capplet. The Screen Resolution capplet will reset the &#8220;`DesktopSetup`&#8221; option in your `/etc/X11/xorg.conf` file to the default of &#8220;`clone`&#8220;.If you&#8217;ve already used the Screen Resolution capplet and don&#8217;t want your desktop cloned, remove the following folder from your home directory:`~/.gconf/desktop/gnome/screen`

I really wish Gnome&#8217;s Configuration Editor would let you delete folders, but just deleting the folder and restarting Gnome works fine.

Thanks to everyone in #gnome on irc.gnome.org who helped me figure this one out!

**Update:** I&#8217;m an idiot. One of the students that uses Linux pointed out to me that the ATI drivers simple use a wider resolution when spanning monitors. So if I add &#8220;2048&#215;768&#8221; to my xorg.conf, the Screen Resolution capplet will work again.

 [1]: http://www.gnome.org/