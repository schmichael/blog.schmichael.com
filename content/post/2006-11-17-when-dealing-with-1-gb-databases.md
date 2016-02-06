---
title: When dealing with 1 GB databases…
author: Michael Schurter
layout: post
date: 2006-11-17
url: /2006/11/17/when-dealing-with-1-gb-databases/
dsq_thread_id:
  - 977109862
categories:
  - Open Source
  - SQL
  - Technology

---
&#8230;create good indexes.

This should be obvious, but for some reason I was getting frustrated with MySQL for taking almost 30 seconds to query a 1 GB table that only had a worthless index on a [surrogate key][1]. With proper indexing, the same query takes less than 1/10th of a second.

 [1]: http://en.wikipedia.org/wiki/Surrogate_key