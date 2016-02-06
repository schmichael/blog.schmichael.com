---
title: Batch Converting OpenOffice.org Files
author: Michael Schurter
layout: post
date: 2007-10-09
url: /2007/10/09/batch-converting-openofficeorg-files/
dsq_thread_id:
  - 469877425
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
There&#8217;s a handy utility called [unoconv][1] that lets you batch/mass convert OpenOffice.org files to any format OpenOffice supports such as PDF, Word DOC, or HTML.

Here&#8217;s how to use it in Linux:

<pre lang="bash">wget http://dag.wieers.com/home-made/unoconv/unoconv-0.3.tar.bz2
tar xjf unoconv-0.3.tar.bz2
cd unoconv
./unoconv --listener &#038;
echo $! > unoconv.pid
# To convert all ODT files in ~/Documents to Word DOC format:
./unoconv -f doc ~/Documents/School/*.odt
kill `cat unoconv.pid`
rm unoconv.pid
</pre>

The two important commands are:

  * `unoconv --listener` &#8211;to start the listener
  * `unoconv -f <em>format path/to/odt/documents</em>` &#8211;to actually convert files

 [1]: http://dag.wieers.com/home-made/unoconv/