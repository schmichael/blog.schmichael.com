---
title: Simple WordPress Upgrade Using Subversion
author: Michael Schurter
layout: post
date: 2007-10-28
url: /2007/10/28/simple-wordpress-upgrade-using-subversion/
dsq_thread_id:
  - 478902716
categories:
  - Open Source
  - PHP
  - Technology
tags:
  - bzr
  - Open Source
  - PHP
  - subversion
  - wordpress

---
I&#8217;ve been using subversion to update WordPress for a few minor revisions now. I simply followed the 2.2 branch and ran&#8230; 

<pre lang="bash">svn up</pre>

&#8230;to update my code.

Today I ran&#8230; 

<pre lang="bash">svn switch http://svn.automattic.com/wordpress/branches/2.3</pre>

&#8230;followed by visiting the upgrade script page and everything worked beautifully!

Anyone _not_ using subversion to update WordPress is doing way too much work! Time to play with tags&#8230;

<small>Now if I was really cool I&#8217;d use <a href="http://bazaar-vcs.org/">bzr</a> to maintain my local code changes and plugins in my own repository&#8230; maybe later.</small>