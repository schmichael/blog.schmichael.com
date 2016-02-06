---
title: Finding Logged In Users by IP using Samba/AD
author: Michael Schurter
layout: post
date: 2006-11-17
url: /2006/11/17/finding-logged-in-users-by-ip-using-sambaad/
dsq_thread_id:
  - 463870243
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology

---
I&#8217;ve created a neat little syslog-ng to MySQL bridge for Tremont School&#8217;s Sonicwall firewall. I wrote it in C# with [some help from the Mono User&#8217;s mailing list][1]. Now I can create realtime reports and pretty graphs on handy data like who&#8217;s using Limewire or what sites blocked by the Sonicwall CFS are being hit.

The big missing feature is finding out who&#8217;s logged into the machine at the local IP address recorded in the log. I&#8217;m not even sure this is possible on an Active Directory network as authentication uses [Kerberos][2]. I&#8217;m betting Microsoft exposes some sort of [DCE][3]/[MSRPC][4] feature for discovering logged in users similar to the Open Sessions information produced by the Computer Manager or _net_ command.

So far the best I can do is the [Samba][5] _nmblookup -A 192.168.0.1_ command which seems to return the currently logged in user as the last row:

<pre>COMPUTER       &lt;00> -         M
DOMAIN         &lt;00> -  M
COMPUTER       &lt;03> -         M
COMPUTER       &lt;20> -         M
DOMAIN         &lt;1e> -  M
USERNAME       &lt;03> -         M</pre>

where COMPUTER = NetBIOS computer name, DOMAIN = AD Domain Name, and USERNAME = currently logged in user (I think). However, using NetBIOS on an Active Directory network seems wrong, and I&#8217;m having trouble confirming the behavior of _nmblookup_.
  
[My post to Samba&#8217;s mailing list][6] has gone pretty much unanswered which is always frustrating. Any ideas are welcome!

 [1]: http://lists.ximian.com/pipermail/mono-list/2006-November/033372.html
 [2]: http://web.mit.edu/kerberos/
 [3]: http://en.wikipedia.org/wiki/Distributed_Computing_Environment
 [4]: http://en.wikipedia.org/wiki/MSRPC
 [5]: http://samba.org
 [6]: http://lists.samba.org/archive/samba/2006-November/127022.html