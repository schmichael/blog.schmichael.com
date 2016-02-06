---
title: Python Packaging Talk
author: Michael Schurter
layout: post
date: 2009-09-09
url: /2009/09/09/python-packaging-talk/
dsq_thread_id:
  - 476224474
categories:
  - Open Source
  - Python
  - Technology
tags:
  - distribute
  - distutils
  - packaging
  - pdxpython
  - pip
  - setuptools
  - slides
  - whereampy

---
I gave a talk at [PDX Python][1] last night on Python Packaging. It&#8217;s just an overview and introduction completely lacking in any practical examples.

  * [Python Packaging slides (ODP)][2]
  * [Python Packaging slides (PDF)][3]

<small>Let me know if the ODP source is messed up. OpenOffice.org liked randomly losing background images and forgetting other formatting.</small>

So as penance I quick hacked up a silly little command line utility and uploaded it to PyPI to serve as a simple packaging example:

  * [whereampy on PyPI][4]
  * [whereampy on bitbucket][5]

It&#8217;d be nice to add some more advanced features like test running, including package data, and building C extensions. If you feel adventurous please [fork][6] it and send me a [pull request][7] on BitBucket.

Thanks to everyone who came to PDX Python last night! Especially [Armin Ronacher][8] who was able to clarify and elaborate on a number of different distutils/setuptools topics!

**Update:** Just spotted [an excellent post on distutils and setuptools by Tarek ZiadÃ©.][9] Make sure to [read his blog if you&#8217;re interested in packaging in Python.][10]

 [1]: http://pdxpython.org/
 [2]: /files/packaging.odp
 [3]: /files/packaging-2.pdf
 [4]: http://pypi.python.org/pypi/whereampy
 [5]: http://bitbucket.org/schmichael/whereampy/
 [6]: http://bitbucket.org/schmichael/whereampy/fork/
 [7]: http://bitbucket.org/schmichael/whereampy/pull/
 [8]: http://lucumr.pocoo.org/
 [9]: http://tarekziade.wordpress.com/2009/09/12/static-metadata-for-distutils/
 [10]: http://tarekziade.wordpress.com/