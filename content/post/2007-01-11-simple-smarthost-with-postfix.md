---
title: Simple Smarthost with Postfix
author: Michael Schurter
layout: post
date: 2007-01-11
url: /2007/01/11/simple-smarthost-with-postfix/
dsq_thread_id:
  - 471215380
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
I wanted to setup my workstation&#8217;s e-mail to relay through the new e-mail server I setup. To do this I would need to setup my workstation&#8217;s Postfix SMTP client to use the mail server as a **relayhost** (Postfix lingo) a.k.a. a **smarthost**.

My e-mail server **requires plaintext authentication and TLS** (self-signed certificate). This is very important because by default Postfix **does _not_ try plaintext authentication or TLS.**
  
My workstation&#8217;s /etc/postfix/main.cf looks like this:

<p style="font-family: monospace">
  smtp_tls_security_level = encrypt # Encryption only because cert is self-signed<br /> relayhost = mail.tremont702.us<br /> smtp_sasl_auth_enable = yes<br /> smtp_sasl_password_maps = hash:/etc/postfix/smtp_sasl_passwd<br /> smtp_sasl_type = cyrus<br /> smtp_sasl_mechanism_filter = plain, login<br /> smtp_sasl_security_options = noanonymous
</p>

Then create the /etc/postfix/smtp\_sasl\_passwd which will hold your e-mail username and password:

<p style="font-family: monospace">
  mail.tremont702.us my_username:MY_PASSWORD
</p>

Make sure your password file is **only readable by root**, and run _postmap /etc/postfix/smtp\_sasl\_passwd_ to create the hash index/database file.

Reload Postfix using _sudo postfix reload_ and all e-mails sent from your workstation will be relayed through your e-mail server!

**Update:**Â  Don&#8217;t forget to install the libsasl2-modules package (for Debian at least)!