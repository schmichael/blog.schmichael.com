---
title: 'Living Dangerously: Using Windows without an AntiVirus'
author: Michael Schurter
layout: post
date: 2006-05-02
url: /2006/05/01/living-dangerously-using-windows-without-an-antivirus/
dsq_thread_id:
  - 463870094
categories:
  - IT
  - Open Source

---
Today was finally able uninstall [McAfee][1]&#8216;s awful Managed VirusScan.  I installed it because a client I worked for a lot had a SonicWall Firewall that required it be installed (or an IP based exception would have to be setup).  Windows XP&#8217;s boot time went from an agonizing few minutes to finally back under a minute.

McAfee&#8217;s definition of &#8220;Managed&#8221; was &#8220;ActiveX&#8221; which meant the installation frequently didn&#8217;t work and much digging through mysterious C:\Windows\ directories was needed to uninstall it, just so you could attempt to reinstall it properly.

Anyway, I&#8217;ve opted to only run [ClamWin][2] which is an open source virus scanner which I&#8217;ve had running on Synthesys&#8217;s mail server for over a year with a 100% block rate.  One catch: no on-demand scanner.

We&#8217;ll see how long I last without a full antivirus product.  Hopefully ClamWin will add on-demand scanning soon&#8230; Maybe this is my chance to learn Python, so I can contribute back to this project!

 [1]: http://www.mcafee.com/
 [2]: http://www.clamwin.com/