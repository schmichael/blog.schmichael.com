---
title: lxml vs. ElementTree
author: Michael Schurter
layout: post
date: 2009-10-14
url: /2009/10/14/lxml-vs-elementtree/
dsq_thread_id:
  - 463870956
categories:
  - Python
  - Technology
tags:
  - benchmarks
  - ElementTree
  - lxml
  - xml

---
While lxml has some [excellent benchmarks about the speed of lxml.etree vs. ElementTree][1], I wanted to run some tests that were as close as possible to my own use case (fairly simple multi-megabyte XML files).

Here are the results of my little test script [lxml-v-etree.py][2] (times are in milliseconds):

<pre>name           generate | tostring | total | write | parse | find | total
------------------------+----------+-------+-------+-------+------+------
xml.cElementTree    132 |   2430   |  2562 |  2433 |   158 |   58 |   216
xml.cElementTree    112 |   2384   |  2497 |  2387 |   158 |   25 |   183
xml.cElementTree    113 |   2393   |  2507 |  2396 |   161 |   25 |   187
xml.ElementTree     591 |   2571   |  3163 |  2574 |  3613 |   25 |  3638
xml.ElementTree     619 |   2567   |  3187 |  2570 |  3589 |   55 |  3644
xml.ElementTree     609 |   2578   |  3188 |  2581 |  3564 |   55 |  3619
lxml                333 |     75   |   409 |    82 |   200 |    0 |   201
lxml                355 |     93   |   448 |    95 |   182 |   32 |   214
lxml                310 |     94   |   404 |    96 |   156 |   56 |   213
------------------------+----------+-------+-------+-------+------+------
name           generate | tostring | total | write | parse | find | total
------------------------+----------+-------+-------+-------+------+------
</pre>

Note that the first &#8220;total&#8221; is &#8220;generate + tostring&#8221; while the second &#8220;total&#8221; is for the 2 parsing related tests (previous 2 columns summed).

My parsing tests are basically &#8220;etree.parse&#8221; and then running &#8220;Element.getchildren()&#8221; 3 times, which is ridiculously simplistic and should probably be ignored. My writing tests are far more thorough/realistic.

I&#8217;m running Python 2.6.2 with lxml 2.1.5 and libxml2 2.6.32 on Ubuntu 9.04 x86_64.

 [1]: http://codespeak.net/lxml/performance.html
 [2]: /files/lxml-v-etree.py-remove-me