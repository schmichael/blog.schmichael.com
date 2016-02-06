---
title: Uglier than SquirrelMail
author: Michael Schurter
layout: post
date: 2007-04-23
url: /2007/04/23/uglier-than-squirrelmail/
dsq_thread_id:
  - 576402231
categories:
  - Open Source
  - Python
  - Technology

---
Over the course of the past few weeks I&#8217;ve periodically hacked on a IMAP web mail application when I&#8217;ve had a few spare minutes.

I setup a mail server at work a while ago and wanted an IMAP capable web mail application to go with it. I really didn&#8217;t want to subject my users to SquirrelMail, so I ended up installing Horde which at least isn&#8217;t an eyesore.

At the same time I was tinkering with Python, specifically: CherryPy, Django, and TurboGears.

While [Django][1] and [TurboGears][2] are impressive web application platforms, neither made sense for a web mail application.

So I give you **[CherryMail][3].** Its interface is ugly. Its code is even uglier. And it doesn&#8217;t have many features.

But as long as you have [Python][4] 2.4, [CherryPy][5] 3, [Genshi][6] 0.4 and a [Dovecot][7] 1.0 RC 15 IMAP server, you can try it out. It may work fine with other setups as well, but thats the environment I used.

And of course its open source, licensed under the BSD license.

I&#8217;ll probably continue to poke at it and will try to get it into a public subversion repository. Feel free to [send me patches][8]!

<small>Disclaimer: I didn&#8217;t want to torture the world with my terrible code, but <a href="http://www.dowski.com/">Christian</a> assured me that any CherryPy sample code is a good thing. So blame him. 😉</small>

 [1]: http://www.djangoproject.com/
 [2]: http://www.turbogears.org/
 [3]: http://michael.susens-schurter.com/code/cherrymail-2007.04.23.tar.bz2
 [4]: http://www.python.org
 [5]: http://www.cherrypy.org
 [6]: http://genshi.edgewall.org/
 [7]: http://www.dovecot.org/
 [8]: mailto:michael+cherrymail@susens-schurter.com