---
title: Windows XP ate my Linux
author: Michael Schurter
layout: post
date: 2005-09-26
url: /2005/09/26/windows-xp-ate-my-linux/
dsq_thread_id:
  - 463869805
categories:
  - Open Source
tags:
  - Personal

---
So everything went great for [my friend who installed Ubuntu on his computer.][1] That is until he attempted to install Windows XP on an empty partition. Windows XP blew away the <acronym title="GRand Unified Bootloader">GRUB</acronym> <acronym title="Master Boot Record">MBR</acronym>, so now he (we, I?) has to figure out how to boot back into Ubuntu (a LiveCD perhaps?) and tell GRUB to rewrite the MBR.

Thanks a lot Microsoft.

 [1]: http://blogs.synthesyssolutions.com/michael/2005/09/20/unbuntu-better-work/