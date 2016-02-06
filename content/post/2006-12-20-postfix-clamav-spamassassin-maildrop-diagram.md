---
title: Postfix + ClamAV + SpamAssassin + Maildrop Diagram
author: Michael Schurter
layout: post
date: 2006-12-20
url: /2006/12/20/postfix-clamav-spamassassin-maildrop-diagram/
dsq_thread_id:
  - 463870299
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology

---
I just finished setting up a new mail server at work. I&#8217;m hoping to replace our current e-mail servers (1 exchange server for internal mail & 1 outsourced for external), so to help sell the idea I wanted to install all of the latest anti-spam solutions.

I ended up choosing [Postfix][1], [clamsmtp][2], [ClamAV][3] (clamd), [SpamAssassin][4] (spamc + spamd), [Maildrop][5], and [Courier-IMAP][6]. I tried using _amavisd-new_ to tie everything together, but it was such a hideous confusing mess I gave up. Using clamsmtp to pass mail to ClamAV works flawlessly and maildrop made using SpamAssassin a 1-line process.

I made a diagram of the whole mail delivery process which you can download as a [PDF][7] or [ODG][8] (OpenOffice.org Draw) document. Sorry if its hideous &#8212; I made this mainly just to wrap my head around what was going on.

Its worth noting that I&#8217;m using all local users and mailboxes (nothing _virtual_). Thanks to winbind, both Postfix and Courier authenticate users against Active Directory. The only thing I haven&#8217;t automated is creating users&#8217; home directories on the server, but thats easily scripted.

 [1]: http://www.postfix.org/
 [2]: http://memberwebs.com/nielsen/software/clamsmtp/
 [3]: http://www.clamav.net/
 [4]: http://spamassassin.apache.org/
 [5]: http://www.courier-mta.org/maildrop/
 [6]: http://www.courier-mta.org/imap/
 [7]: http://michael.susens-schurter.com/blog/wp-content/uploads/2006/12/mail-server-diagram.pdf
 [8]: http://michael.susens-schurter.com/blog/wp-content/uploads/2006/12/mail-server-diagram.odg