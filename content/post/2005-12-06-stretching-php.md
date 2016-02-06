---
title: Stretching PHP
author: Michael Schurter
layout: post
date: 2005-12-06
url: /2005/12/06/stretching-php/
dsq_thread_id:
  - 649588020
categories:
  - PHP
tags:
  - Synthesys

---
My last post probably deserves a little more elaboration about what I&#8217;m busy doing. Currently I&#8217;m working on an internal PHP project that uses PHP in ways most people would find frightening:

  * Real Time
  * Mission Critical
  * High Security

Before you write me off as another crazy PHP zealot stretching PHP far beyond where it was meant to go, let me explain.

This project pulls data from two sources: one XML and one CSV. Both bits of data are posted via HTTP. Apache handles all the security for me using SSL certificates for the server **and clients**, and I also limit access based on client IP.

I **have** to rely on Windows scheduling to run a PHP script once a minute to post the CSV to another server (also running PHP). However, even in a completely unrealistic stress test, the script executed in only 9 seconds (normally executes in under 3).

And finally to address the mission critical part: with the exception of the Windows computers that have to post CSVs, my main server runs Linux with all the nice self-monitoring goodies installed (Webmin&#8217;s system monitoring, smartd, etc.). It&#8217;s been up for over 150 days, and it would have been up for its entire life if not for a faulty UPS. Even when it unexpectedly went down, it came right back up and didn&#8217;t lose any data.

So while common knowledge might suggest using PHP for mission critical, real time, high security systems is crazy, my experience has shown PHP is easily up to the task.