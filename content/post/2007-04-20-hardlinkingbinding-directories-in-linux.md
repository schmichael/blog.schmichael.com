---
title: Hardlinking/Binding Directories in Linux
author: Michael Schurter
layout: post
date: 2007-04-20
url: /2007/04/20/hardlinkingbinding-directories-in-linux/
dsq_thread_id:
  - 471354236
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
The `mount --bind <em>source</em> <em>target</em>` command links one folder to another. For example I put an extra drive in a Linux box that I want to store a specific folder on. I may store some other folders on it, and I really don&#8217;t want to have to partition it ahead of time. Basically I just want an easy way to move folders to it as needed.

However, the mount command doesn&#8217;t persist across reboots. So instead I add lines like the following to /etc/fstab:

`/mnt/drive2/firewall-log   /var/log/firewall-log   auto   bind   0   0`

To get the new mount to work immediately simply type:

`sudo mount -a`

This is also a handy way to create shared folders among multiple users.

If I were really cool, I&#8217;d learn how to use [LVM][1], but binding directories is just so quick and easy.

 [1]: http://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux)