---
title: TokyoCabinet + fapws3 = tc-rest
author: Michael Schurter
layout: post
date: 2009-08-09
url: /2009/08/08/tokyocabinet-fapws3-tc-rest/
dsq_thread_id:
  - 468006009
categories:
  - Open Source
  - Python
  - Technology
tags:
  - fapws3
  - Python
  - tc-rest
  - tokyo cabinet

---
Have you ever wondered how hard it would be to tack a RESTful HTTP interface on top of a fast key/value database like TokyoCabinet?

Probably not, but I did: [tc-rest.tar.gz][1]

Components:

  * [TokyoCabinet][2] &#8211; my favorite persistent key/value database
  * [pytc][3] &#8211; a wonderful Python wrapper for TC
  * [fapws3][4] &#8211; a fast libev based HTTP/[WSGI][5] server
  * [simpleson][6] &#8211; (or Python >= 2.6) for encapsulating HTTP responses
  * [okapi][7] &#8211; a fantastic little static HTML page for testing HTTP APIs

Getting TokyoCabinet+pytc to work inside a [virtualenv][8] was a bit tricky, so check out my `run.sh` script if you&#8217;re having trouble getting it to start.

Once you get it started, load okapi in your browser:

<http://localhost:8080/static/okapi.html>

And then create a database by doing a POST like:

`http://localhost:8080/foo/`

And finally store/get keys and values using GET and POST requests like:

`http://localhost:8080/foo/bar/`
  
`http://localhost:8080/foo/baz/`

Doing a GET request to a database URL lists keys.

At any rate, I had big dreams for building a system where you would store JSON, specify indexes on certain keys, and the server would maintain those indexes for you by creating ad hoc TokyoCabinet databases.

Instead I ended up wasting most of my time learning how to write a low-level WSGI app. I should have just used CherryPy or Django from the beginning, but I had never written a pure WSGI app before. It was a good lesson even if it meant not getting some of my features implemented.

I&#8217;ll probably keep playing with this idea, but the next version will probably be based on some existing framework. Parsing `environ['PATH_INFO']` and running `start_response(...)` manually gets old fast.

fapws3 is pretty neat, but had lots of annoying rough edges. I had to manually create a `README` file because its setup.py expects one to exist. Then I had to manually allow DELETE HTTP methods in fapws/base.py, otherwise it would return an HTML error message for me! That was a bit shocking since I was working under the assumption fapws3 is just a low-level HTTP/WSGI server.

**Update**

  1. [If you&#8217;re new to TokyoCabinet, I posted my presentation on it that I did at Portland Python meetup][9].
  2. Someone want to benchmark this for me? Might be interesting since its made with the fastest libs available in Python for their respective tasks. I&#8217;m just feeling lazy at this point. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

 [1]: /files/tc-rest.tar.gz
 [2]: http://tokyocabinet.sourceforge.net/
 [3]: http://pypi.python.org/pypi/pytc/
 [4]: http://github.com/william-os4y/fapws3/tree/master
 [5]: http://www.python.org/dev/peps/pep-0333/
 [6]: http://code.google.com/p/simplejson/
 [7]: http://www.aminus.net/wiki/Okapi
 [8]: http://pypi.python.org/pypi/virtualenv/
 [9]: http://michael.susens-schurter.com/blog/2009/03/11/tokyo-cabinet-pytyrant-talk/