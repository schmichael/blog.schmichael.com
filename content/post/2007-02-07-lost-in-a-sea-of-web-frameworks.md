---
title: Lost in a Sea of Web Frameworks
author: Michael Schurter
layout: post
date: 2007-02-07
url: /2007/02/07/lost-in-a-sea-of-web-frameworks/
dsq_thread_id:
  - 463870360
categories:
  - Mono/.Net
  - Open Source
  - PHP
  - Technology

---
So I&#8217;ve been trying to learn Python and have successfully written a couple small scripts. For the couple of small web sites/services I&#8217;ve written, I used CherryPy mostly because I know someone who is active in the CherryPy community.Coming from PHP and ASP.NET, Python&#8217;s offerings of web frameworks are a bit confusing. Here is my impression of the general landscape of the 3 platforms:

  * [PHP][1] &#8211; A language which survived without widely adopted frameworks for many years. While many frameworks are gaining popularity, most major PHP applications are their own framework.
  
    Examples: [Drupal][2] (a CMS) and [Horde][3] (a framework and suite of web applications)
  * [ASP.NET][4] &#8211; The web framework bundled with Microsoft&#8217;s monolithic .NET platform. Supports multiple languages and even implementations ([go Mono!][5]). A few alternative web frameworks exist for .NET ([Castle Project][6]), but it seems much more popular to just build components on top of ASP.NET.
  * [Python][7] &#8211; While I&#8217;m still learning a lot about Python, it seems Python has a wide variety of frameworks which range from a complete web application stack including database and kitchen sink ([Zope][8]) to just a widgets toolkit ([ToscaWidgets][9]) or just an HTTP/object-dispatching framework ([CherryPy][10]).

Then there are the various Javascript/DHTML/AJAX client side frameworks which can replace the interface portions of the above platforms and frameworks. It seems to me these UI frameworks have caused PHP-sans-a-framework to remain popular because the server-side code becomes a simple data broker for the complex UI widgets.

Python is obviously a bit different than PHP and ASP.NET. While using a framework seems the norm (unlike constantly rolling your own in PHP), there&#8217;s no 1-framework-to-rule-them-all like ASP.NET.

Luckily my web applications have been very simple, so CherryPy by itself has worked fine. I may even go the hackish route of just using a Javascript UI framework to keep my Python code simple. I&#8217;ve been trying to learn a little more about [TurboGears][11] and ToscaWidgets as well, but so far I haven&#8217;t needed a full framework.

 [1]: http://php.net/
 [2]: http://drupal.org
 [3]: http://www.horde.org/
 [4]: http://asp.net
 [5]: http://www.mono-project.com/
 [6]: http://www.castleproject.org/
 [7]: http://www.python.org/
 [8]: http://www.zope.org/
 [9]: http://toscawidgets.org/
 [10]: http://www.cherrypy.org/
 [11]: http://www.turbogears.org/