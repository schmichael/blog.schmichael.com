---
title: Fedora’s Crypto Consolidation
author: Michael Schurter
layout: post
date: 2008-10-20
url: /2008/10/20/fedoras-crypto-consolidation/
dsq_thread_id:
  - 463870776
categories:
  - GNU/Linux
  - Open Source
  - Technology
tags:
  - crypto
  - debian
  - fedora
  - security
  - ubuntu

---
I just found out Fedora is attempting to consolidate on [Mozilla&#8217;s NSS][1] for [system-wide cryptography][2]. I love the idea and hope it succeeds as it will make using crypto so much easier for system administrators and users.

Since humans are the weakest link in the security chain, improving the human interaction with crypto is a much bigger security win than the latest impossible-to-crack-by-the-NSA-in-a-bajillion-years algorithm. While switching libraries isn&#8217;t exactly a huge UI win, having a single application to manage all of your certificates, keys, passwords, etc. would be.

I&#8217;d love to see Debian, Ubuntu, Suse, et al, get on board as well because this is the sort of initiative that simply won&#8217;t happen upstream. Upstream developers have already chosen a crypto library and probably like it. The burden of tight integration is definitely the job of system engineers and packagers.

I submitted an Ubuntu Brainstorm Idea, so please feel free to vote on it if you&#8217;re so inclined:
  
[![][3]][4]

I would love to submit this idea to Debian as well, but I have no idea where to even start. Probably a mailing list, but I don&#8217;t exactly have the skills to defend this proposition. Eventually bugs would need to be filed against every package that needs to be converted to NSS, but I&#8217;m afraid doing that as just-another-end-user might just anger a bunch of maintainers&#8230;

**Update:** Looks like the [LSB is standardizing on NSS][5] as well.

<small>I <em>really</em> need to learn deb packaging&#8230;</small>

 [1]: http://developer.mozilla.org/en/NSS
 [2]: http://fedoraproject.org/wiki/FedoraCryptoConsolidation
 [3]: http://brainstorm.ubuntu.com/idea/14632/image/1/
 [4]: http://brainstorm.ubuntu.com/idea/14632/
 [5]: http://ldn.linuxfoundation.org/article/lsb-beta-reveals-new-tools-features-developers