---
title: Every 3rd Safari Upload Fails
author: Michael Schurter
layout: post
date: 2007-10-17
url: /2007/10/17/every-3rd-safari-upload-fails/
dsq_thread_id:
  - 463870581
categories:
  - Python
  - Technology
tags:
  - cherrypy
  - Lo-Fi Art
  - safari

---
<div style="float: left;">
  <a href="http://cherrypy.org"><img src="http://michael.susens-schurter.com/files/cplogo.jpg" alt="CherryPy Logo" /></a>
</div>

Recently I built a small [CherryPy][1] application to allow users to upload photos to a gallery. The application is pretty trivial and just uses the [Python Imaging Library][2] to resize the photos and [Genshi][3] to output some XML which is used by a Flash gallery.

However, after deployment a user complained every 3rd upload would fail. She was using Safari on Mac OSX, and I couldn&#8217;t duplicate the error in Firefox. Luckily she didn&#8217;t mind switching to Firefox and it fixed her problem:

> Working with Firefox has helped tremendously! I&#8217;ll only use it from now on, and we should be fine with uploads. 

Has anyone else seen this? I [deployed CherryPy behind Apache 2.2 using mod_proxy][4], and Apache logs the following error when an upload fails (IPs changed):

<pre>[error] proxy: client 000.000.000.000 given Content-Length did not match number of body bytes read
[error] (70014)End of file found: proxy: pass request body failed to 127.0.0.1:9595 (127.0.0.1) from 00.000.000.001 ()</pre>

So it appears Safari just messes up the Content-Length. All CherryPy would receive is a POST with no data.

 [1]: http://cherrypy.org/
 [2]: http://www.pythonware.com/products/pil/
 [3]: http://genshi.edgewall.org/
 [4]: http://michael.susens-schurter.com/blog/2007/08/16/deploying-cherrypy-on-apache-2-using-mod_proxy/