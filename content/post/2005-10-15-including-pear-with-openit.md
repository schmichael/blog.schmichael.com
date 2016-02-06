---
title: Including PEAR with OpenIT
author: Michael Schurter
layout: post
date: 2005-10-15
url: /2005/10/15/including-pear-with-openit/
dsq_thread_id:
  - 475816303
categories:
  - Open Source
tags:
  - OpenIT

---
OpenIT now seems to do the same thing a number of other PHP projects do: bundle PEAR packages.

I made a script to make keeping PEAR in OpenIT up-to-date simple: [openitPEAR.php][1] This script is for developer use only, and allows developers to run regular PEAR commands within OpenIT&#8217;s PEAR environment. Therefore to upgrade all of OpenIT&#8217;s PEAR packages, you just run `./openitPEAR.php upgrade-all`

It may be handy for other PHP projects that wish to bundle PEAR packages. The source is quite easy to read besides some bash-isms left over from my first attempt to write it as a shell script.

What&#8217;s scary is that eventually this script + a PEAR channel could equal modular OpenIT. Meaning OpenIT could be split up into PEAR modules and installed via the openitPEAR.php script. This idea seems more of a could-do than a will-do.

 [1]: http://cvs.sourceforge.net/viewcvs.py/openit/OpenIT/tools/openitPEAR.php?view=markup