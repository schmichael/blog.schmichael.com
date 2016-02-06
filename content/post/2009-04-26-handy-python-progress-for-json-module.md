---
title: Handy Python Progress for JSON module
author: Michael Schurter
layout: post
date: 2009-04-26
url: /2009/04/26/handy-python-progress-for-json-module/
dsq_thread_id:
  - 463870901
categories:
  - Open Source
  - Python
  - Technology
tags:
  - json

---
I&#8217;ve been spending a good deal of time the past couple of days processing large JSON files to try and fix some corrupted data (long story, short version: my fault). While JSON is a fast file format to work with, processing > 50 MB of any data format takes some time.

So to give myself some idea of what was going on, I whipped up a small progress bar for Python 2.6&#8217;s [json][1] module (works on [simplejson][2] if you&#8217;re still using 2.4/2.5):

<pre lang="python">import sys

class JsonProgress(object):
    def __init__(self):
        self.count = 0

    def __call__(self, obj):
        self.count += 1
        sys.stdout.write("\r%8d" % self.count)
        return obj
</pre>

And then use it as the object_hook when loading JSON:

<pre lang="python">f = open('foo.json')
foo = json.load(f, object_hook=JsonProgress())
print "\rDone" # \r in the next line erases the progress output
</pre>

Although JsonProgress is a poor name since its also useful in generic list comprehensions:

<pre lang="python">progress = JsonProgress()
foo = [progress(x) for x in bar]
print "\nDone" # \n prints a newline so the progress output is kept
</pre>

Obviously this is a performance hit, but still quite handy for personal use when you just want to know that _something_ is happening.

 [1]: http://docs.python.org/library/json.html
 [2]: http://pypi.python.org/pypi/simplejson