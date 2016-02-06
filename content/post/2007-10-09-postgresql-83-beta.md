---
title: PostgreSQL 8.3 Beta
author: Michael Schurter
layout: post
date: 2007-10-09
url: /2007/10/09/postgresql-83-beta/
dsq_thread_id:
  - 712474851
categories:
  - Open Source
  - PostgreSQL
  - SQL
  - Technology

---
<small>Warning: <abbr title="I Am Not A DataBase Administrator">IANADBA</abbr></small>
  
I was just reading the [release notes for PostgreSQL 8.3 beta1][1], and there&#8217;s quite a lot of exciting improvements coming:

  * Full text search is now a built-in feature
  * Support for the SQL/XML standard, including a new xml builtin data type _(For the enterprisy users)_
  * enum data types _(I&#8217;m not a big fan of enums in a database, but lots of people like them.)_
  * UUID data type, similar to that defined by [RFC 4122][2]. _(Very useful feature in some clustering situations. Some people even argue GUIDs/UUIDs should replace integer surrogate keys most of the time.)_
  * ORDER BY &#8230; NULLS FIRST/LAST _(A minor little feature, but I remember wishing for it once upon a time.)_
  * And some excellent performance improvements, especially if you&#8217;re data doesn&#8217;t have to be flushed to disk to finish a transaction (potentially dangerous, but acceptable for many use cases).

While I haven&#8217;t had the pleasure of using PostgreSQL for a few months, I prefer it over MySQL and recommend it to anyone looking for an open source database with advanced features and excellent reliability.

 [1]: http://www.postgresql.org/docs/8.3/static/release-8-3.html
 [2]: http://www.ietf.org/rfc/rfc4122.txt