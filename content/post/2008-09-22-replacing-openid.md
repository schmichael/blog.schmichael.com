---
title: Replacing OpenID
author: Michael Schurter
layout: post
date: 2008-09-22
url: /2008/09/22/replacing-openid/
dsq_thread_id:
  - 463870770
categories:
  - Open Source
  - Technology
tags:
  - openid

---
OpenID has admirable goals: reducing the number of accounts you have to create and manage on the Internet. However, as I mentioned in my last post I&#8217;m a bit disappointed with how OpenID has worked in The Real World (that place that doesn&#8217;t care how pretty your APIs are).

So I thought I&#8217;d recommend an alternative: e-mail authentication.

Here&#8217;s how it works:

  1. Enter a comment on a blog with all the usual info: name, _e-mail_, an optional URL, and the comment.
  2. Receive an e-mail with a link that has a unique verification ID.
  3. Click the link, pass an optional CAPTCHA, and your comment is approved.
  4. Receive a cookie containing something like `hash("secret"+email)`, so you don&#8217;t have to re-verify every time you comment.

**Making it better**

Add a Jabber field as an alternative to e-mail. Only require the user to enter one or the other.

**What am I missing?**

This all seems way too simple of a solution, so I&#8217;m guessing there&#8217;s something I fundamentally don&#8217;t understand about OpenID. Good old e-mail verification just seems like a mechanism even your average user-who-uses-the-same-password on every site can understand.