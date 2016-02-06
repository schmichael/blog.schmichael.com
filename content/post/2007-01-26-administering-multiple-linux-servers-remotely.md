---
title: Administering Multiple Linux Servers Remotely
author: Michael Schurter
layout: post
date: 2007-01-26
url: /2007/01/26/administering-multiple-linux-servers-remotely/
dsq_thread_id:
  - 473396523
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology

---
So I was playing around with [recordMyDesktop,][1] and I decided I might as well make something useful with it.

[Administering Multiple Linux Servers Remotely][2] ([ogg][3] format)

If you can&#8217;t play Ogg Theora video files, [download VLC][4] &#8211; it can play anything (or get Linux 😉 ).

Anyway, what I&#8217;m demonstrating here is how I setup drawers and launchers on my Gnome panel to start Synaptic and a Terminal on the remote servers I administer. What makes this really handy is that I don&#8217;t have to login as SSH support Kerberos, and since all of my Linux computers are granted tickets by Active Directory: **Single Sign-On Nirvana**. (Many many thanks to _Earl Tom_ for patiently helping me get SSO setup initially.)

To accomplish all of this beautiful remote administration magic requires getting your Linux boxes to authenticate against Active Directory _**or**_ _just using SSH keys_.

Make sure you have the following settings in your /etc/ssh/sshd_config file:

<p style="font-family: monospace">
  # If you&#8217;re using AD instead of key pairs:<br /> GSSAPIAuthentication yes<br /> # Make sure X Windows programs (like Synaptic) will run:<br /> X11Forwarding yes
</p>

Happy hacking, and let me know if I should record more videos! (Or if you know of a better video recorder than recordMyDesktop. It works perfectly, but Ogg Theora isn&#8217;t a very common codec.)

 [1]: http://recordmydesktop.sourceforge.net/
 [2]: /files/remote_administration.ogg
 [3]: http://www.theora.org/
 [4]: http://www.videolan.org/