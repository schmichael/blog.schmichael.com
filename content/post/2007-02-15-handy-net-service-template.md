---
title: Handy .Net Service Template
author: Michael Schurter
layout: post
date: 2007-02-15
url: /2007/02/15/handy-net-service-template/
dsq_thread_id:
  - 535607727
categories:
  - GNU/Linux
  - IT
  - Mono/.Net
  - Open Source
  - Technology

---
I love .Net Services. Its a handy way to create background processes, and they work beautifully in both Windows and Linux (thanks to Mono!).

However, every time I create one I find myself writing a lot of the same code with minor variations:

  * OnStart: start a worker thread, make it sure it didn&#8217;t die, exit
  * OnStop: try to stop the worker thread nicely, wait, abort it, exit

Depending on how &#8220;nice&#8221; you want to be to your worker thread, you can come up with some pretty crazy code to deal with your worker thread (volatile class variables, wait loops, etc.).

I&#8217;ve created a basic template for new .Net Services:

[ServiceTemplate (2007-02-15)][1]{#p186}

It was inspired by a service I wrote to read a firewall log file into a database:

[Lumberjack (2007-02-15)][2]{#p187}

The template doesn&#8217;t contain any complex worker thread stopping code. _Lumberjack_ uses a mess of methods to try and nicely stop the worker. I&#8217;m not sure what Lumberjack does is really any more useful than just using Abort(), but I didn&#8217;t want to leave a database connection open.

Both zips contain MonoDevelop solution files, although Main.cs is the only important file in both of them.

The other highlight of both the template and Lumberjack is the _SmartLog()_ method which logs to syslog in Linux and the Event Log in Windows. Although you probably have to comment out the syslog reference to build the source in Windows.

I&#8217;m sure I&#8217;ll update and keep using this code in the future&#8230; I need to find some way to manage my mini-projects and code snippets&#8230; any ideas?

 [1]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/02/servicetemplate-20070215.zip
 [2]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/02/lumberjack-20070215.zip