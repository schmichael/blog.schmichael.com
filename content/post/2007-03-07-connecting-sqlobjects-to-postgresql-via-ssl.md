---
title: Connecting SQLObjects to PostgreSQL via SSL
author: Michael Schurter
layout: post
date: 2007-03-07
url: /2007/03/07/connecting-sqlobjects-to-postgresql-via-ssl/
dsq_thread_id:
  - 650717384
categories:
  - Open Source
  - PostgreSQL
  - Python
  - SQL
  - Technology

---
I&#8217;m trying to learn [TurboGears,][1] but I got stumped yesterday trying to figure out how to connect to PostgreSQL via SSL.

Turns out this works in [SQLObject][2] (TurboGear&#8217;s default ORM):

`sqlobject.dburi="postgres://username:pass@servername/mydb sslmode=require"`

Turns out the syntax I was trying to use works with [SQLAlchemy][3] (which it appears most cool kids use):

`postgres://username:pass@servername/mydb``<strong>?</strong>sslmode=require`

Notice the only difference is the question mark between the database and extra parameters. Kind of makes me want to cry&#8230;

To all my friends who have listened to me extol the virtues of Python, let me also add that **learning a new framework sucks**. Especially when that framework is a moving target.

 [1]: http://www.turbogears.org/
 [2]: http://www.sqlobject.org/
 [3]: http://www.sqlalchemy.org