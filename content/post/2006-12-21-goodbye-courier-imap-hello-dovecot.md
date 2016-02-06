---
title: Goodbye Courier-IMAP, Hello Dovecot
author: Michael Schurter
layout: post
date: 2006-12-21
url: /2006/12/21/goodbye-courier-imap-hello-dovecot/
dsq_thread_id:
  - 463870307
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
While putting the finishing touches on [the new mail server I blogged about before][1], I got fed up with [Courier-IMAP][2] and went with [Dovecot][3] instead. I wish I could tell you all kinds of technical reasons why Dovecot is superior, but I don&#8217;t know any.

In fact Courier probably has a lot more features than Dovecot, but one look at the plethora of configuration files in /etc/courier and I ran. Dovecot is well documented, and I only had to change 2 settings from their defaults. What more could you ask for?

**Update:** Dovecot just got even better! I just realized I can [use Dovecot for Postfix&#8217;s SASL authentication][4] instead of running the separate saslauthd daemon! Very easy to setup as well.

 [1]: http://michael.susens-schurter.com/blog/2006/12/20/postfix-clamav-spamassassin-maildrop-diagram/
 [2]: http://www.courier-mta.org/imap/
 [3]: http://www.dovecot.org/
 [4]: http://www.postfix.org/SASL_README.html#server_dovecot