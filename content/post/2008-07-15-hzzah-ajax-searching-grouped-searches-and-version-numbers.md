---
title: 'Hzzah: AJAX Searching, Grouped Searches, and Version Numbers'
author: Michael Schurter
layout: post
date: 2008-07-16
url: /2008/07/15/hzzah-ajax-searching-grouped-searches-and-version-numbers/
dsq_thread_id:
  - 503494657
categories:
  - Uncategorized
tags:
  - ajax
  - boss
  - bzr
  - hzzah
  - hzzah.com
  - jquery
  - yahoo

---
**AJAX Searching**

Thanks to [jQuery][1] and the [jQuery History plugin][2], searching is now done via AJAX but it doesn&#8217;t break your back and forward buttons.

The navigation callback in JavaScript ought to be more of a proper state machine, but considering there are only 3 states (blank, about, and searching) I&#8217;m not too concerned.

**Grouped Searches**
  
I played around with hzzah a bit more after I noticed its search results were far worse than those on Yahoo.com

It seems Yahoo.com only returns 1 or 2 hits per domain, whereas the BOSS API will happily return hundreds all from the same site.

This means if you&#8217;re vain like me and search for your name, you get pages of links to your blog and nowhere else. The [Yahoo.com results are pretty good][3] and only return 2 hits for my blog.

So I grouped hits by domain name, but since I broke pagination in the process, [searching for myself][4] is completely worthless now.

I have some ideas on how to fix that, but they&#8217;ll have to wait for another time.

**Version Numbers**

Squint at the bottom of the page to see the current revision number.

Anybody know how to have that increment automatically when I do `bzr up` on my server? I haven&#8217;t looked for a post-update hook which would do the trick.

 [1]: http://docs.jquery.com/Ajax
 [2]: http://plugins.jquery.com/project/history
 [3]: http://search.yahoo.com/search?p=michael+schurter&ei=UTF-8&fr=
 [4]: http://hzzah.com/#s:michael%20schurter