---
title: CherryMail and Fun with AJAX
author: Michael Schurter
layout: post
date: 2007-05-07
url: /2007/05/07/cherrymail-and-fun-with-ajax/
dsq_thread_id:
  - 476829460
categories:
  - Open Source
  - Python
  - Technology

---
I&#8217;ve hacked a bit more on CherryMail, my web mail for IMAP project. I&#8217;ve never really played around with any of the fancy new JavaScript frameworks out there, so I quick slapped some [DataTables][1] from [Yahoo&#8217;s UI Library][2] into CherryMail.

The result is actually a slower interface, but the addition of AJAX had interesting implications on my code layout. I now have 1 controller module (controller.py) for serving mostly static HTML, and all of the IMAP controller logic has been moved into a second controller (jsoncontroller.py) that outputs [JSON][3] for my JavaScript widgets to digest.

Not exactly useful at this point, but I found it interesting to basically use AJAX as the primary data connector.

If you really feel like torturing your eyes with my code, feel free to grab it here:

[CherryMail 2007.05.07][4]

Or grab the latest source from my Subversion repository:

<http://michael.susens-schurter.com/cherrymail/svn/trunk/>

My subversion repository ended up being as messy as my code, but I&#8217;ve always found the process of importing source into a new subversion repository a bit clumsy.

Speaking of clumsy, I&#8217;ve been using [Eclipse][5] and [PyDev][6] for development, so I thought I might as well try [Subclipse][7] as well. While Subclipse seems very feature complete, I find myself dropping to the command line to use the old svn command because Eclipse is just so clumsy and slow.

Its like using a forklift to move furniture in your house: perfectly capable, but a bit more hassle than its worth.

 [1]: http://developer.yahoo.com/yui/datatable/
 [2]: http://developer.yahoo.com/yui/
 [3]: http://www.json.org/
 [4]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/05/cherrymail-20070507.tar.gz "CherryMail 2007.05.07"
 [5]: http://www.eclipse.org/
 [6]: http://pydev.sourceforge.net/
 [7]: http://subclipse.tigris.org/