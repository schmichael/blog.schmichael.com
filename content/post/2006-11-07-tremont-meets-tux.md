---
title: Tremont meets Tux
author: Michael Schurter
layout: post
date: 2006-11-08
url: /2006/11/07/tremont-meets-tux/
dsq_thread_id:
  - 1085345702
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology

---
For a number of good reasons, [Tremont School][1]&#8216;s use the standard Windows Active Directory + Exchange + Windows Workstations infrastructure. Even though I&#8217;m one of those crazy Linux zealots I understand that 1 guy managing 500 machines doesn&#8217;t exactly have time to learn and implement an upstart operating system.

However, now that its 2 guys managing 500 machines, its my goal to start using Linux where appropriate (aka everywhere 😉 ).

I&#8217;ve now done what I&#8217;ve always dreamed of doing: **use Linux as my primary operating system at work.**

Here&#8217;s the my setup:

  * [Debian Etch][2] (tried [Ubuntu Edgy Eft][3], but it felt too&#8230; pretty.)
  * [pam\_winbind + pam\_krb5 for authentication][4]
  * [Evolution][5] for e-mail and calendaring &#8211; **integrates seamlessly with Exchange** including contacts & calendars! I can&#8217;t tell you how impressed with Evolution I am. I&#8217;m not entirely sure why more people don&#8217;t use it instead of [Thunderbird][6]. Evolution even has [Windows support][7] now.
  * [Samba][8] + [CUPS][9] for File and Print Sharing
  * [OpenOffice.org][10] (obviously)

I have also installed [WINE][11] + [IE6][12] thinking that I might try to install MS Office in the future just so I use the same productivity suite as everyone else, but so far I haven&#8217;t needed to worry about it.

 [1]: http://www.tremont702.org/
 [2]: http://www.debian.org/releases/etch/
 [3]: http://www.ubuntu.com/news/610released
 [4]: http://michael.susens-schurter.com/blog/2006/11/07/authenticating-against-active-directory-in-linux/
 [5]: http://www.gnome.org/projects/evolution/
 [6]: http://www.mozilla.com/en-US/thunderbird/
 [7]: http://shellter.sourceforge.net/evolution/
 [8]: http://samba.org
 [9]: http://www.cups.org/
 [10]: http://www.openoffice.org/
 [11]: http://www.winehq.com/
 [12]: http://www.tatanka.com.br/ies4linux/page/Main_Page