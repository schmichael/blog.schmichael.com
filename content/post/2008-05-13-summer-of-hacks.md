---
title: Summer of Hacks
author: Michael Schurter
layout: post
date: 2008-05-13
url: /2008/05/13/summer-of-hacks/
dsq_thread_id:
  - 463870722
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology
tags:
  - denyhosts
  - hacking
  - linode
  - ssh

---
My [Linode][1] has been experiencing a huge number of brute force login attempts in the past week. I don&#8217;t keep detailed statistics, but I would guess there have been **300 attempts in the past week** as opposed to _the usual rate of about 500 attempts over 200 days (2-3 attempts per day)_.

[Denyhosts][2] has been doing its job perfectly. It should be illegal to run a Internet exposed SSH server without it or a similar tool.*

Thanks to HoopyCat in #linode for pointing me to a [SANS Internet Storm Center article explaining the _Summer of Hacks_][3] phenomenon. 

<small>* Unless of course you only accept key based logins.</small>

 [1]: http://www.linode.com/
 [2]: http://denyhosts.sourceforge.net/
 [3]: http://isc.sans.org/diary.html?storyid=4408