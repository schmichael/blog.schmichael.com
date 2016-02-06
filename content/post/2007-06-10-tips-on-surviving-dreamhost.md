---
title: Tips on Surviving DreamHost
author: Michael Schurter
layout: post
date: 2007-06-11
url: /2007/06/10/tips-on-surviving-dreamhost/
dsq_thread_id:
  - 463870486
categories:
  - GNU/Linux
  - PHP
  - Python
  - Technology
tags:
  - Personal

---
I use DreamHost and it is by far the _**least**_ **reliable hosting service I&#8217;ve ever used.**

However, they&#8217;re quite cheap for the vast amounts of storage and bandwidth provided. I also **love** their [blog][1], newsletter, [status page][2], control panel, and especially that they&#8217;re [green][3]!

Bottom line: DreamHost is great for some use cases, and incredibly dangerous for others. Here are some tips:

  1. **Do** **_not_ use IMAP for DreamHost e-mail.** IMAP is wonderful&#8230;at least over a 100% reliable high-bandwidth, low-latency connection. I would recommend only using DreamHost for POP access or e-mail forwarding.
  
    I made the mistake of using IMAP and now have over 5,000 wonderfully organized and filtered messages trapped on DreamHost&#8217;s unreliable servers. I&#8217;m not a big fan of Gmail&#8217;s non-hierarchical organization scheme, and both Yahoo! & Hotmail have miserable user interfaces. So now I&#8217;m stuck with embarrassingly unreliable e-mail acces.
  2. **Do _not_ store any sensitive information on DreamHost.** They just had a [security breach][4].
  
    If you do, make sure that the file permissions only allow your user access to sensitive files: `chmod 0600 <em>filename</em>`
  3. **Do _not_ host sites which require high levels of availability.** You&#8217;ve been warned. 😉

Enough bad news, here&#8217;s what I do recommend using DreamHost for:

  1. Personal sites (like my blog) or sites which don&#8217;t require high availability (small businesses or organizations).
  2. Serving static media files for a site hosted elsewhere (although some sort of failover should be used).
  3. Remote backup &#8212; as long as you **encrypt any sensitive information**.
  4. Shell access to a Linux server. If you want to play with Linux + Apache + MySQL + [PHP][5]/[Perl][6]/[Ruby on Rails][7]/[Python][8], DreamHost seems like an excellent choice. Just remember to move to a more reliable hosting service before launching your Web 2.0 startup.

 [1]: http://blog.dreamhost.com/
 [2]: http://www.dreamhoststatus.com/
 [3]: http://www.dreamhost.com/green.cgi?susens-schurter.com
 [4]: http://www.dreamhoststatus.com/2007/06/06/security-breach/
 [5]: http://www.php.net/
 [6]: http://www.perl.org/
 [7]: http://www.rubyonrails.org/
 [8]: http://www.python.org/