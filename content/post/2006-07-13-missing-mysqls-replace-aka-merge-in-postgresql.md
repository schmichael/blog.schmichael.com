---
title: Missing MySQL’s REPLACE (aka MERGE) in PostgreSQL
author: Michael Schurter
layout: post
date: 2006-07-13
url: /2006/07/13/missing-mysqls-replace-aka-merge-in-postgresql/
dsq_thread_id:
  - 465006333
categories:
  - Mono/.Net
  - Open Source
  - PostgreSQL
  - SQL
  - Technology

---
When Synthesys first decided to go with PostgreSQL as the database for a large web application, I was very excited to get away from our usual reliance on MySQL and move to a _real_ database platform.

Once we figured out the whole MySQL auto_increment vs. [PostgreSQL SERIAL][1], the first thing we really missed in PostgreSQL was the REPLACE statement. I understand why its missing, and it is kind of a hack of a SQL statement (its not in a SQL standard).

Turns out in the [SQL 2003 Standard there is a statement similar to REPLACE called MERGE][2]. Despite PostgreSQL&#8217;s excellent support for standards, they [have not implemented MERGE][3]. I would guess it has something to do with the ambiguity of the statement.

At any rate I still love working with PostgreSQL, and for what its worth [Npgsql is an excellent PostgreSQL connector for Mono/.Net][4]. (Even in RC/Beta state)

 [1]: http://www.postgresql.org/docs/8.1/interactive/datatype.html#DATATYPE-SERIAL
 [2]: http://www.varlena.com/GeneralBits/73.php
 [3]: http://www.postgresql.org/docs/8.1/interactive/unsupported-features-sql-standard.html
 [4]: http://pgfoundry.org/projects/npgsql/