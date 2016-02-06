---
title: VNC Server on Debian 3.1 (Sarge)
author: Michael Schurter
layout: post
date: 2006-02-03
url: /2006/02/03/vnc-server-on-debian-31-sarge/
dsq_thread_id:
  - 463869988
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
Recently [Deloy][1] asked me for help setting up VNC on some [Fedora][2] servers his students are using. While I&#8217;ve never used Fedora, the setup I use in [Debian][3] [Sarge][4] should work on any sensible Linux distribution (and probably any good *nix machine). This setup will allow multiple users to login concurrently.
  
The packages I use:

  * tightvncserver 1.2.9 <small>(plain old vncserver works, but tightvncserver has better compression)</small>
  * vnc-common 3.3.7
  * x11vnc 0.7
  * netkit-inetd 0.10 <small>(any sort of inetd/xinetd implementation should work)</small>

**1. Append to `/etc/services`:**

`custom-vnc    5951/tcp`

Note: There&#8217;s nothing magical about port 5951, specify whatever port you want.)

**2. Append to `/etc/inetd.conf`:**

`custom-vnc   stream  tcp     nowait  nobody.tty      /usr/bin/Xvnc Xvnc -inetd -query localhost -once -geometry 800x600 -depth 16`

Note: Tweak the geometry & depth settings depending on the bandwidth you have available. Don&#8217;t be afraid to specify non-traditional geometries like 800&#215;1000 to get the best fit for your desktop.

**3. Restart inetd.** In Debian I usually use the bizarre &#8220;invoke-rc.d inetd restart&#8221; command although a good &#8220;/etc/init.d/inetd restart&#8221; accomplishes the same task. For some reason I&#8217;ve always thought the invoke-rc.d method was preferred, but I have no clue where I got that idea from.

**4. Connect remotely.** On another computer open up your favorite VNC viewer and point it to the hostname and port (port not Display number) of the server you just setup VNC server on.

You should see your default X Windows Display Manager login screen (probably [gdm][5] for [Gnome][6] or kdm for [KDE][7]). You can now login and use that computer remotely. Simply logout when you&#8217;re finished.

**Caveat:** As far as I know you cannot share a single VNC session among multiple viewers, but that feature of VNC doesn&#8217;t make much sense in this context.

<span style="font-weight: bold">Tip:</span> While the <span style="font-style: italic">Tight</span> encoding supported by many VNC clients and servers offers JPEG compression which is great for low-bandwidth connections. However, Tight encoding takes a lot more processing time than other encodings and the compression is [lossy][8], so stick to the simpler encodings for LAN connections.
  
<span style="font-weight: bold" />

<span style="font-weight: bold">Warning:</span> <span style="font-style: italic">The VNC protocol is not secure. Please use a VPN or secure tunneling protocol like <a href="http://www.openssh.org/">SSH</a> when using VNC.</span>

 [1]: http://www.greenville.edu/faculty/dcole/
 [2]: http://fedora.redhat.com/
 [3]: http://www.debian.org/
 [4]: http://www.debian.org/releases/sarge/
 [5]: http://www.gnome.org/projects/gdm/
 [6]: http://www.gnome.org/
 [7]: http://www.kde.org/
 [8]: http://en.wikipedia.org/wiki/Lossy_compression