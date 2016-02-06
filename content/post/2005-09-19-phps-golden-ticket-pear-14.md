---
title: 'PHP’s Golden Ticket: PEAR 1.4'
author: Michael Schurter
layout: post
date: 2005-09-19
url: /2005/09/19/phps-golden-ticket-pear-14/
dsq_thread_id:
  - 956997100
categories:
  - PHP
tags:
  - OpenIT

---
[PEAR 1.4][1] has been been released! I hope features like channels, mirroring support, remote installation, and improved dependencies support will help fuel wide spread adoption and innovation of this wonderful piece of software.

I&#8217;ll be honest, I&#8217;m very frustrated with PHP&#8217;s current habit of BC breakage. I&#8217;ve been using Mono/.Net a lot at [work][2] and [school][3], and it&#8217;s so nice to program in a language that is not only cross-platform, but is also source **and** binary compatible between two different implementations of the C# and runtime standard. PHP can&#8217;t stay self-compatible between minor version numbers!

However, I still prefer developing web applications in PHP as the development and deployment is so much easier than messing with xsp, mod-mono, or IIS (\*shudder\*).

Maybe at some point in the future I&#8217;ll create a PEAR package for OpenIT, so I can tell people to just run `pear upgrade-all` to cure all their woes. But first, I&#8217;d better get 2.0.1 out&#8230;

 [1]: http://pear.php.net/package/PEAR/download/
 [2]: http://www.synthesyssolutions.com
 [3]: http://www.greenville.edu