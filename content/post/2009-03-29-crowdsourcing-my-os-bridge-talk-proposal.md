---
title: Crowdsourcing my OS Bridge Talk Proposal
author: Michael Schurter
layout: post
date: 2009-03-30
url: /2009/03/29/crowdsourcing-my-os-bridge-talk-proposal/
dsq_thread_id:
  - 513601236
categories:
  - GNU/Linux
  - Open Source
  - Technology
tags:
  - osbridge

---
**Update:** [Submitted my proposal][1], but please still leave me comments! I can still edit my proposal.

Web server performance has been a hot topic for some time now as Apache hasn&#8217;t been the only viable option for a few years.

I want to do a talk at [OS Bridge][2] doing practical comparisons between the popular web site hosting options available today. There&#8217;s plenty of requests per second comparisons between the major HTTP servers out there, so I want to go beyond and compare a wide variety of metrics in a wide variety of environments.

Here&#8217;s what I&#8217;m thinking so far, but **I&#8217;d love your feedback!** I&#8217;m really excited about the possibility of presenting at a large conference like OS Bridge and want to make my talk as exciting and useful as possible.

**Metrics**

  * Requests per second (serially* and concurrent)
  * Memory usage
  * Features (extensibility, modularity, etc)
  * Community (support options, tools/modules available, etc)
  * Portability
  * Reliability (can I crash it? how well does it handle load?)
  * Ease of setup and maintenance (floods of patches? hideous config file?)

**Web Servers**

The usual suspects (will definitely test):

  * [Apache][3] 2.2 (prefork _and_ worker mpms)
  * [Nginx][4] 0.6.x (latest stable)
  * [Lighttpd][5] 1.4.x (latest stable)

Maybes:

  * Nginx 0.5.x (legacy)
  * Nginx 0.7.x (latest dev)
  * [Cherokee][6] (not sure if its really popular enough yet to bother)
  * [CherryPy][7] and some other language specific or just less known servers would be fun.
  * IIS &#8211; It&#8217;d be really fun if I could find someone willing to help me run my tests on IIS. I definitely won&#8217;t be setting it up myself though!

**Test Cases**

This is where things become _really_ complicated. I don&#8217;t want to just download static files from each server and pretend like thats a real world use case, but at the same time the various environments I could come up with are nearly limitless.

I want to strive to cover the most common environments** as well as a few variations that produce interesting results.

  * [WordPress][8] (mod-php where applicable and FastCGI)
  * [Drupal][9] (mod-php where applicable and FastCGI)
  * Bugzilla, Redmine, and Trac (to test a few non-trivial apps from 3 popular languages)
  * trivial [Django][10] app (mod-python & mod-wsgi on Apache, FastCGI everywhere)
  * trivial [Ruby on Rails][11] app (need advice from RoR devs on common deployment methods)
  * trivial Zend Framework app (or is there a more popular php framework?)
  * something from the Java world?
  * maybe something fairly obscure like [Seaside][12]?

**Conclusion**

Wow, that seems like a lot to cover thoroughly, but I think the research will be a lot of fun to do.

Please let me know your thoughts either in the comments, on [twitter (@schmichael)][13], on [IRC (schmichael again)][14], or via [e-mail][15].

* * *

<small><br /> * Its interesting to compare <em>serial</em> to <em>parallel</em> req/sec to give people an idea of how well the technology will scale <em>on a single server</em>. I&#8217;ll make sure to note good serial performance can often be turned into good parallel performance by using a load balancing proxy and multiple instances of your application server.<br /> ** All Linux based for simplicity unless someone volunteers to run the tests on other platforms.<br /> </small></p>

 [1]: http://opensourcebridge.org/proposals/119
 [2]: http://opensourcebridge.org/
 [3]: http://httpd.apache.org/
 [4]: http://nginx.net/
 [5]: http://www.lighttpd.net/
 [6]: http://www.cherokee-project.com/
 [7]: http://www.cherrypy.org
 [8]: http://wordpress.org/
 [9]: http://drupal.org/
 [10]: http://www.djangoproject.com/
 [11]: http://rubyonrails.org/
 [12]: http://www.seaside.st/
 [13]: http://twitter.com/schmichael
 [14]: http://opensourcebridge.org/2009/03/open-source-bridge-is-on-irc/
 [15]: mailto:michael+osbridge@susens-schurter.com