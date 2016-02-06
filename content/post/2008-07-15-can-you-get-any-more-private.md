---
title: Can you get any more private?
author: Michael Schurter
layout: post
date: 2008-07-16
url: /2008/07/15/can-you-get-any-more-private/
dsq_thread_id:
  - 807423489
categories:
  - Technology
tags:
  - apache
  - hzzah
  - hzzah.com
  - jquery
  - privacy

---
I just switched [Hzzah.com][1]&#8216;s Apache configuration to use this line for logging:

`CustomLog /srv/hzzah/log/access.log "0.0.0.0 %l %u %t \"%r\" %>s %b"`

No more IP addresses logged! Only if you cause an error (404 or 500) will your IP address be logged.

So no javascript, css, or images from remote sites; no cookies; no ads. Can you get any more private?

I did just add jQuery and a bit of JavaScript, so if web2.0 makes you queasy, you&#8217;ve been warned.

<small>I should mention that hzzah&#8217;s primary goal is for me to have fun with Django, not privacy. So while I&#8217;ll definitely warn you if I make any changes, right now its not a top priority to pursue extreme privacy.</small>

 [1]: http://hzzah.com