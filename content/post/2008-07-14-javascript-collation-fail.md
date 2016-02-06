---
title: JavaScript Collation Fail
author: Michael Schurter
layout: post
date: 2008-07-14
url: /2008/07/14/javascript-collation-fail/
dsq_thread_id:
  - 464120734
categories:
  - Technology
tags:
  - i18n
  - javascript
  - l10n
  - localecompare
  - unicode
  - utf8
  - webdev

---
In JavaScript, the [localeCompare method on Strings][1] seems like a great way to properly sort strings, but its not:
  
[![localeCompare Javasript method in 4 browsers][2]][2]
  
_Hint: The last line should all look the same._ At least I expect Firefox and Opera to agree. You can&#8217;t expect much from IE6.

For kicks [try out other browsers][3] and post the final sorted list in the comments (hopefully my blog supports unicode).

**Updated 2012-05-16:** Hilariously a coworker stumbled across this page, so I updated the MDN link as Mozilla had broken it.

 [1]: https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String/localeCompare
 [2]: http://michael.susens-schurter.com/files/localecompare-x-browser.png
 [3]: http://michael.susens-schurter.com/files/localecompare.html