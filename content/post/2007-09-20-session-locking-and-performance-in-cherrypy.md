---
title: Session Locking and Performance in CherryPy
author: Michael Schurter
layout: post
date: 2007-09-20
url: /2007/09/20/session-locking-and-performance-in-cherrypy/
dsq_thread_id:
  - 463979659
categories:
  - Open Source
  - Python
  - Technology

---
While working on that firewall project [I keep alluding to][1], I came across an interesting caveat when using sessions (tools.sessions) and static file directories (tools.staticdir):

Sessions are locked on a per-request basis meaning while a request is being processed, all other requests _by that session_ will **block** until the lock is released (by default at the end of the response handler).

This is a **Very Good Thing**, at least as the default behavior. Its the only safe way to automatically handle sessions.

However, this can become a performance problem, especially for those of us addicted to tabbed browsing. Take this trivial app as an example:

<pre lang="python">#!/usr/bin/python
import cherrypy, time

class Test:
    @cherrypy.expose
    def page1(self):
        # Simulate long operation
        time.sleep(20)
        return "*Yawn*"

    @cherrypy.expose
    def page2(self):
        return "Hello World!"

cherrypy.config.update({
    'tools.sessions.on': True, 
    'tools.sessions.storage_type': 'ram'})
cherrypy.quickstart(Test(), '/')
</pre>

Start it up, and then go to these pages in order in 2 different tabs:

  1. <http://localhost:8080/page1>
  2. <http://localhost:8080/page2>

**You&#8217;ll notice that page2 doesn&#8217;t load until page1 is finished loading!** This effectively limits sessions to 1 request at a time. For many web sites this might not be an issue. However, for complex web applications which might be doing time consuming operations on the server, this could give users the impression the server has crashed.

Fortunately this is a very easy issue to resolve. The best way is to do [explicit session locking manually.][2]

However, if implicit session locking works for you most of the time you can sneak in a `cherrypy.session.release_lock()` into your code Like this:

<pre lang="python">#...snip...
    @cherrypy.expose
    def page1(self):
        # Do any session manipulation here!
        cherrypy.session.release_lock()
        # Simulate long operation
        time.sleep(20)
        return "*Yawn*"
#...snip...
</pre>

Now hit [page1][3] and [2][4] again and notice that page2 loads immediately!

<small>At <a href="http://technogeek.org/">Kevin&#8217;s</a> <a href="http://michael.susens-schurter.com/blog/2007/09/18/a-lesson-on-python-dns-and-threads/#comment-12731">suggestion</a> I turned off the visual editor in WordPress. I had thought of this before, but couldn&#8217;t find where the option to disable it was! Evidently its a per-user setting which makes sense.</p> 

<p>
  At any rate, WordPress seems to be leaving my whitespace alone now! Thanks Kevin!</small>
</p>

 [1]: http://michael.susens-schurter.com/blog/2007/09/18/a-lesson-on-python-dns-and-threads
 [2]: http://cherrypy.org/wiki/CherryPySessions#Lockingsessions
 [3]: http://localhost:8080/page1
 [4]: http://localhost:8080/page2