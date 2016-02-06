---
title: Debian Etch Released
author: Michael Schurter
layout: post
date: 2007-04-08
url: /2007/04/08/debian-etch-released/
dsq_thread_id:
  - 463870443
categories:
  - GNU/Linux
  - Mono/.Net
  - Open Source
  - PHP
  - PostgreSQL
  - Python
  - Technology

---
It [appears][1] [Debian GNU/Linux 4.0, codenamed Etch,][2] (quite a mouthful) [has been released as the latest stable version of Debian][3].

Go [download it using BitTorrent to be cool][4]. 😉

**Tip #1:**Â  You do _**not**_ have to download all of the CDs, just get one and Debian&#8217;s installer will download the rest.)

I&#8217;m a happy and loyal Debian user and strongly encourage any Linux power users to try out Etch. [Ubuntu][5] is still my recommendation for users who want things to &#8220;Just Work.&#8221; However, I highly recommend Debian for any kind of server (file, print, application, database, web, e-mail).

**Tip #2:** Check out [Debian Multimedia][6] for all of your proprietary codec needs!

**Mini-Review**

I&#8217;ve been using Etch (and Sid) for a while now, so its tough to do a real review from a &#8220;normal&#8221; end user&#8217;s perspective.

Some highlights:

  * Developer&#8217;s should be happy as [PHP,][7] [Python][8], [Mono,][9] [MySQL,][10] and [PostgreSQL][11] are all fairly up-to-date and extremely easy to install.
  * [Gnome][12] is stable and speedy.
  * The [graphical installer][13] brings Debian out of the 1990s and offers tons of features.
  * As usual, Debian&#8217;s package repository is _huge_. Forget vendor-supplied RPMs or custom installers, if its not in Debian&#8217;s repository (or Debian Multimedia), you probably don&#8217;t need it. 😉

Some downsides:

  * Relatively ancient version of the standard C library (2.3.6) means [poor compatibility with 3rd party binaries][14] (which Debian has always hated anyway).
  * Gnome is 2 stable versions behind in Debian (2.14 vs. 2.18). This is very frustrating as Gnome constantly produces nice incremental improvements.
  * Debian just isn&#8217;t as easy to use by default as Ubuntu. Debian needs to install and integrate some of the more cutting edge desktop apps like [Beagle][15], [Tomboy][16], [Deskbar][17], and Ubuntu&#8217;s nicer package management interfaces.
  * [Secure APT][18] is a _great_ feature, but the error messages it can produce are going to scare the pants off of new users. More effort needs to be made to integrate all of the various places user&#8217;s encounter public key crypto. Right now its very schizophrenic and confusing: GPG errors are too common, and command line magic that even confuses me is necessary to add new repositories.
  * Not related to the release, Debian&#8217;s support system is a confusing jumble of web interfaces, mailing lists, IRC channels, and [an excellent wiki][19] (that I rarely remember to use). Hopefully this is something a new [Debian DPL][20] will address.

 [1]: http://www.debian-administration.org/articles/514
 [2]: http://www.debian.org/releases/etch/releasenotes
 [3]: http://www.debian.org/News/2007/20070408
 [4]: http://www.debian.org/CD/torrent-cd/
 [5]: http://www.ubuntu.com/
 [6]: http://www.debian-multimedia.org/
 [7]: http://php.net/
 [8]: http://python.org/
 [9]: http://mono-project.com/
 [10]: http://mysql.com/
 [11]: http://www.postgresql.org/
 [12]: http://www.gnome.org/
 [13]: http://wiki.debian.org/DebianInstaller/GUI
 [14]: http://thomas.apestaart.org/log/?p=457
 [15]: http://beagle-project.org
 [16]: http://www.gnome.org/projects/tomboy/
 [17]: http://raphael.slinckx.net/deskbar/
 [18]: http://wiki.debian.org/SecureApt
 [19]: http://wiki.debian.org
 [20]: http://wiki.debian.org/DebianProjectLeader?action=show&redirect=DPL