---
title: I Love Linode
author: Michael Schurter
layout: post
date: 2007-08-16
url: /2007/08/15/i-love-linode/
dsq_thread_id:
  - 470965885
categories:
  - GNU/Linux
  - IT
  - Technology

---
I just signed up for a new [Linode][1] account. This is the fourth account I&#8217;ve created with them over the years, and I&#8217;ve always been very pleased. I wish I do a side-by-side comparison with another [VPS][2] host, but I&#8217;ve never had any reason to shop around.

<small>I guess I did administer a Windows 2003 VPS on <a href="http://www.godaddy.com/">GoDaddy</a> for a while. The experience was too horrific to even try to compare to Linode. Why anyone would want a Windows web server is beyond me. At the time we had been fooled into using ASP.NET to build a huge web application. I&#8217;ll never make that mistake again.</small>

Linode is a VPS provider which uses [User Mode Linux][3] to create virtual Linux servers which run as a process on top of a physical Linux server. While [Xen][4] seems to be the one getting all of the hype these days, UML is extremely stable, secure, and mature. Each user is allocated a pool of [IO tokens][5] which refills at a static rate. This allows servers to have high burst IO rates while preventing any single virtual server from hogging the IO. It seems to work quite well.

Registration was quick and easy. My only minor complaint is that there&#8217;s about an hour wait between when you&#8217;re billed and when you&#8217;re account is activated. When I asked their support about this I got a fast reply from Thomas Asaro:

> Every signup is manually reviewed and approved by staff. This is to prevent fraudulent signups, protect the credit card holders, and protect our network. Our average activation time is 1 hour.

That&#8217;s probably my favorite thing about Linode: **excellent support.** Whether its via e-mail, their [wiki][5], [IRC][6], or [forums][7], the Linode staff and users have always been quick to help.

I started using Linode years ago when I worked for [Synthesys Solutions][8]. At the time we were using some terrible shared hosting provider that was constantly having problems. We decided not to risk our luck with another shared hosting provider, and I configured a Linode for hosting our web sites and e-mail.

The only performance issues I had with Linode were caused by spam. We scanned all of our e-mail for viruses with [ClamAV][9]. While ClamAV is a fantastic solution, like all virus scanners its very resource intensive. So a spam bomb would hit our server and bring it to an unusable crawl for anywhere from 30 minutes to over an hour. A faster Linode would have helped, but administering an e-mail server is always going to be a constant battle (unless you don&#8217;t care about your users).

For now I plan on still using DreamHost for e-mail hosting to avoid the spam battle. While the stability isn&#8217;t what I would like, POP3 users rarely, if ever, notice. And right now I don&#8217;t host enough e-mail addresses to warrant the headache of managing it myself.

I highly recommend Linode to anyone looking for an extremely reliable Linux hosting service who doesn&#8217;t want to spend a lot on a dedicated server.

 [1]: http://www.linode.com/
 [2]: http://en.wikipedia.org/wiki/Vps
 [3]: http://user-mode-linux.sourceforge.net/
 [4]: http://www.xensource.com
 [5]: http://www.linode.com/wiki/index.php/IO_Tokens
 [6]: http://www.linode.com/irc/
 [7]: http://www.linode.com/forums
 [8]: http://www.synthesyssolutions.com/
 [9]: http://www.clamav.net/