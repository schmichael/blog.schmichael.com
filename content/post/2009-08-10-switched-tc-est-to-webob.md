---
title: Switched tc-rest to webob
author: Michael Schurter
layout: post
date: 2009-08-11
url: /2009/08/10/switched-tc-est-to-webob/
dsq_thread_id:
  - 463870933
categories:
  - Open Source
  - Python
  - Technology
tags:
  - bitbucket
  - fapws3
  - Python
  - tc-rest
  - tokyo cabinet

---
Small update on my toy tc-rest project: I switched to using [WebOb][1] for creating HTTP Request and Response objects. Cleaned up the code a bit, but a real dispatcher is what&#8217;s needed to really remove the cruft.

I&#8217;m anxious to extend the API and add features, but I have no clue when I&#8217;ll have time to touch it again. In the mean time I&#8217;ve [pushed tc-rest to bitbucket.org if you want to take a look][2].

 [1]: http://pythonpaste.org/webob/
 [2]: http://bitbucket.org/schmichael/tc-rest/overview/