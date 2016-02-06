---
title: PostgreSQL 8.2 Released
author: Michael Schurter
layout: post
date: 2006-12-06
url: /2006/12/06/postgresql-82-released/
dsq_thread_id:
  - 487112519
categories:
  - Open Source
  - PostgreSQL
  - SQL
  - Technology

---
Just noticed [PostgreSQL 8.2 was released yesterday][1]. I chose PostgreSQL 8.x for a large project when MySQL 5 either wasn&#8217;t out or was too new for my comfort.

I learned database application programming on MySQL, but now I choose PostgreSQL whenever I have the option. PostrgeSQL is just packed with features that MySQL either doesn&#8217;t have or just recently implemented so you need a cutting edge version.

It seems to me that PostgreSQL has a much better user community as well. I know there are many excellent DBA&#8217;s using MySQL, but the MySQL community seems dominated by PHP hackers who found MySQL pre-installed on their $5/mo. shared hosting account.

If you&#8217;ve never tried PostgreSQL, I highly recommend it, especially if you&#8217;ve ever implemented _autonumber tables_ in MySQL to get around flaky autonumber generation. PostgreSQL uses _sequences_ which are basically single field/row tables for maintaining autonumbers. There are a number of [sequence related functions in PostgreSQL][2] that makes work with autonumbers not only easy, but also predictable.

Oh and [pgAdmin III][3] beats MySQL&#8217;s awkward and buggy GUI offerings any day.

 [1]: http://www.postgresql.org/docs/8.2/static/release-8-2.html
 [2]: http://www.postgresql.org/docs/8.2/interactive/functions-sequence.html
 [3]: http://www.pgadmin.org/