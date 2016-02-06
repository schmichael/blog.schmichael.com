---
title: Introducing Hzzah!
author: Michael Schurter
layout: post
date: 2008-07-15
url: /2008/07/15/introducing-hzzah/
dsq_thread_id:
  - 463870743
categories:
  - Open Source
  - Python
  - Technology
tags:
  - boss
  - bzr
  - django
  - google
  - hzzah
  - hzzah.com
  - opensource
  - Python
  - yahoo

---
<small>from the I-can-haz-a-search-engine department&#8230;</small>

**Update:** Sorry about the tacky donate link all. I tried to hide it from feed readers with WordPress&#8217;s <!&#8211;more> feature, but evidently that doesn&#8217;t apply to feeds. <img src="http://localhost/wp-includes/images/smilies/frownie.png" alt=":(" class="wp-smiley" style="height: 1em; max-height: 1em;" />

When it comes to market share, Google is to Searching as Microsoft is to Operating Systems. Thankfully Google has won their dominant position by creating a really amazing product <small>(you can find plenty of discussions on <a href="http://en.wikipedia.org/wiki/Criticism_of_Microsoft#Business_practices">why Microsoft is on top elsewhere)</a></small>.

Recently [Yahoo! opened up their search APIs][1] for anyone to use along with [a handy Python library][2]. In a time when Yahoo&#8217;s very existence is being threatened, I felt a pang of nostalgia for the search engine that fed me decent results for &#8220;free dos games&#8221; throughout the mid-90s.

So last night I whipped up a little search engine called [Hzzah!][3]*

<div style="clear: both; line-height: 0px; font-size: 0px;">
  &nbsp;
</div>

<div style="float: right; clear: both;">
  <a href="http://creativecommons.org/licenses/BSD/"><img src="http://michael.susens-schurter.com/files/40bsd.png" alt="BSDtastic!" /></a>
</div>

**Features:**

  * Simple
  * No ads, cookies, or even JavaScript <small>(at the moment at least)</small>
  * Open Source! [BSD to be precise][4].
  * Did I mention simple? That&#8217;s really all it has going for it&#8230;

<!--more-->

If you have [Bazaar][5] installed you can grab the code a variety of ways:

<pre lang="bash"># If you know Subversion, use this method.  `bzr up` will keep you up to date
bzr checkout http://michael.susens-schurter.com/code/hzzah-public

# If you want to hack on Hzzah or are comfortable with bzr, feel free to branch
bzr branch http://michael.susens-schurter.com/code/hzzah-public hzzah-steve
</pre>

You can also [grab a zip][6], but its probably going to become out of date quickly.

_Read the README file for help setting it up._

And like I say in the README, if you&#8217;re feeling generous, feel free to toss some cash this way:
  
[<img src="https://www.paypal.com/en_US/i/btn/btn_donate_SM.gif" border="0" alt="PayPal - The safer, easier way to pay online!" />][7]

<small>* Make fun of the name all you like&#8230; there&#8217;s no good domain names left. The name is inspired by a friend from college for whom <em>huzzah</em> was her exclamation of choice.</small>

 [1]: http://developer.yahoo.com/search/boss/
 [2]: http://developer.yahoo.com/search/boss/mashup.html
 [3]: http://hzzah.com
 [4]: http://creativecommons.org/licenses/BSD/
 [5]: http://bazaar-vcs.org/
 [6]: http://michael.susens-schurter.com/code/hzzah-public-r5.zip
 [7]: https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=mschurter%40yahoo%2ecom&item_name=hzzah%2ecom%20by%20Michael%20Schurter&item_number=1337&no_shipping=0&no_note=1&tax=0&currency_code=USD&lc=US&bn=PP%2dDonationsBF&charset=UTF%2d8