---
title: Deploying Python behind Nginx Talk Slides
author: Michael Schurter
layout: post
date: 2011-01-25
url: /2011/01/25/deploying-python-behind-nginx-talk-slides/
dsq_thread_id:
  - 464216442
categories:
  - GNU/Linux
  - Open Source
  - Python
  - Technology
tags:
  - nginx
  - pdxpython
  - presentation
  - slides
  - wsgi

---
I gave a talk on deploying Python WSGI apps behind [nginx][1] at the [Portland Python User Group][2] meeting on January 11th and finally got around to publishing the slides: [schmingx][3].

I should mention [Jason Kirtland][4] informed me after the meeting that [FastCGI][5] supports [persistent connections (and a host of other features)][6] between a load balancer and backend app servers.

 [1]: http://wiki.nginx.org/
 [2]: http://wiki.python.org/moin/PortlandPythonUserGroup
 [3]: https://docs.google.com/present/edit?id=0Ab7GDIugV1qCZGR6c3d6YnJfMTA1aGRtZmJxYzI&hl=en
 [4]: http://discorporate.us/jek/
 [5]: http://www.fastcgi.com/devkit/doc/fcgi-spec.html
 [6]: http://www.fastcgi.com/devkit/doc/fcgi-spec.html#S3.5