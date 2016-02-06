---
title: Planned Obsolescence… in 8000 Years
author: Michael Schurter
layout: post
date: 2006-03-22
url: /2006/03/22/planned-obsolescence-in-8000-years/
dsq_thread_id:
  - 463870069
categories:
  - IT
  - SQL

---
I made a simple little real time data reporting system live today which dumps a row into a MySQL database once a minute. I didn&#8217;t include any archiving or purging functionality, so I decided to do some quick calculations to see how long this system could run before running into constraints.

The table uses an unsigned 32-bit integer surrogate key, so in about 8171 years I&#8217;ll run out of unique sequential IDs.

The tables uses about 200 bytes/row, so in 8000 years I&#8217;ll need almost 800 GBs of storage.

The current partition the database is stored on only has 21 GB of free space, so it looks like I&#8217;ll run out of storage space in a mere 200 years.

Of course, the server in question is a Dell, so it will most likely die from hardware failure in a year or two anyway. So much for 8000 years of maintenance free bliss.