---
title: Fun with SQLObject and mxDateTime
author: Michael Schurter
layout: post
date: 2007-11-30
url: /2007/11/29/fun-with-sqlobject-and-mxdatetime/
dsq_thread_id:
  - 463990432
categories:
  - Open Source
  - Python
  - SQL
  - Technology
tags:
  - cherrypy
  - mxdatetime
  - Python
  - sqlobject
  - xml

---
I&#8217;m working on a small [CherryPy][1] web service that among other things saves timestamps to a database. The timestamp is in [RFC 3339][2] format (like `2007-07-31T16:05:00.000-05:00`), and I needed to store the timezone.

Luckily [mxDateTime][3] and SQLObject&#8217;s DateTimeCol both support full dates with times and time zone. Unfortunately its not immediately obvious from [SQLObject&#8217;s lackluster documentation][4] how to use mxDateTime instead of Python&#8217;s built-in datetime.

A little searching brought me to a mailing list post about [how to use mxDateTime by default in SQLObject][5]. (I don&#8217;t know why the sample code includes the conditional as I would think you&#8217;d want your code to outright fail if you&#8217;re unable to use the datetime library you expect.)

So my model&#8217;s code looks something like this:

<pre lang="python">from sqlobject import *
from sqlobject import col

col.default_datetime_implementation = MXDATETIME_IMPLEMENTATION

class Foo(SQLObject):
    timestamp = DateTimeCol(default=DateTimeCol.now)
</pre>

Then my parsing code looks something like this:

<pre lang="python">import model
from mx import DateTime

timestamp = '2007-07-31T16:05:00.000-05:00'
bar = model.Foo(timestamp=DateTime.DateTimeFrom(timestamp))
print 'UTC Timestamp:', bar.timestamp
print 'Local Timestamp:', bar.timestamp.localtime()
</pre>

Basically once you use the magic line `col.default_datetime_implementation = MXDATETIME_IMPLEMENTATION`, everything Just Works.

 [1]: http://cherrypy.org
 [2]: http://www.ietf.org/rfc/rfc3339.txt
 [3]: http://www.egenix.com/products/python/mxBase/mxDateTime/
 [4]: http://sqlobject.org/SQLObject.html
 [5]: http://pythonpaste.org/archives/message/20070410.064412.fa195fb7.en.html