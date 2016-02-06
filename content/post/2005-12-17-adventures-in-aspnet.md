---
title: Adventures in ASP.Net
author: Michael Schurter
layout: post
date: 2005-12-17
url: /2005/12/17/adventures-in-aspnet/
dsq_thread_id:
  - 977221568
categories:
  - Mono/.Net
  - PHP
tags:
  - Synthesys

---
Lately, [Aaron][1] and I have been hacking on a [Synthesys][2] product that uses an ASP.Net Web Service to act as a sort of a proxy between two remote client applications. It&#8217;s been a long and interesting road, especially since until recently the product was something we only used internally and hacked on occassionally.

So the poor web service has been bounced from [Apache][3]+[mod-mono][4] on Linux to [XSP][5] on Linux to IIS6 on Windows 2003 Server (the horror!), and now I&#8217;m secretly porting it back to [XSP2][6] on Linux.

The exerpeince has been as interesting and educational as it has been frustrating. Both Aaron and I have used [PHP][7] pretty exclusively in the web sphere and Visual Studio.Net (C# & VB.Net) on the client side. Here are some things we ran into:

  * Don&#8217;t try to learn ASP.Net using Linux+XSP unless you start from a working example.
  * Don&#8217;t assume anything from PHP applies to ASP.Net.
  * Every feature you need in [Mono][8] is currently in [Subversion][9]. You can check it out, build it from source, and use it, but by the time its officially released you&#8217;ll find you need something new from Subversion.
  * For help with Mono check [Monologue][10], Google, [mailing lists][11], and [the official web sit][12]e. Answers to your questions/problems are evenly divided between these sources.
  * IIS6 is evil, Visual Studio.Net is mysterious and tempermental, but they&#8217;re still easier to learn ASP.Net in than Linux+Mono+XSP+MonoDevelop. (Although [MonoDevelop][13] does rock.)
  * PHP may have its critics, but its still the easiest platform to write web applications in from start to production deployment. (I&#8217;m not saying PHP is the best for every job; I&#8217;m just defending my old loyal friend from detractors.)
  * Debugging a web service thats passing messages between multiple clients is going to be hell no matter what platform you&#8217;re using.
  * Good old fashioned [logging][14] is the most useful debugging tool. (Just the most annoying to implement.)

 [1]: http://blogs.synthesyssolutions.com/aaron/
 [2]: http://www.synthesyssolutions.com/
 [3]: http://httpd.apache.org/
 [4]: http://www.mono-project.com/ASP.NET#Apache_Hosting_with_Mod_Mono
 [5]: http://www.mono-project.com/ASP.NET#XSP
 [6]: http://svn.myrealbox.com/viewcvs/trunk/xsp/?rev=54567
 [7]: http://www.php.net/
 [8]: http://www.mono-project.org/
 [9]: http://svn.myrealbox.com/
 [10]: http://www.go-mono.com/monologue/
 [11]: http://www.mono-project.com/Mailing_Lists
 [12]: http://www.mono-project.com/
 [13]: http://www.monodevelop.com/
 [14]: http://logging.apache.org/log4net/