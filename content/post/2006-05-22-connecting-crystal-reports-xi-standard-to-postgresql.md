---
title: Connecting Crystal Reports XI Standard to PostgreSQL
author: Michael Schurter
layout: post
date: 2006-05-22
url: /2006/05/22/connecting-crystal-reports-xi-standard-to-postgresql/
dsq_thread_id:
  - 463870122
categories:
  - IT
  - Open Source
  - PostgreSQL
  - SQL
  - Technology

---
At [Synthesys][1] we&#8217;re using [PostgreSQL][2] as the database for a large web application.ï¿½ For the time being we&#8217;re writing our reports in Crystal Reports, although we&#8217;re hoping to move to a free platform in the future.

Unfortunately we only have [Crystal Reports XI _**Standard Edition**_][3] which evidently doesn&#8217;t support ODBC connections.ï¿½ Crystal wants you to buy the Professional Edition to get that kind of _enterprise_ functionality.

Our first attempt to get the two talking consisted of using **Microsoft Access&#8217;s External Table Linking capability**.ï¿½ While this was **horrifying** in concept, it actually worked beautifully until you needed to sort by a PostgreSQL _text_ field.ï¿½ Microsoft Access read _text_ fields as _memo_ fields, and you can&#8217;t sort by _memo_ fields.

So back to the drawing board.ï¿½ Our next attempt was to use [**PgOleDb**][4] in hopes that Crystal allowed that.ï¿½ For some reason Crystal allows OLE connections, but not ODBC.ï¿½ However, whenever we tried to add a table to a report, we received an OLE/ADO error.ï¿½ Have I mentioned I hate Window&#8217;s data access technologies?ï¿½ Well I do.

Our final attempt consisted of connecting to **ODBC through OLE**.ï¿½ I don&#8217;t know why this is possible, but it is.ï¿½ Not only is it possible, but it works beautifully.

For some bizarre reason **you can connect to a PostgreSQL database from Crystal Reports XI Standard Edition if you use an OLE wrapper around a PostgreSQL ODBC connection.**

Many thanks to [psqlODBC][5], and no thanks to Crystal.

 [1]: http://www.synthesyssolutions.com/
 [2]: http://www.postgresql.org/
 [3]: http://www.businessobjects.com/products/reporting/crystalreports/standard/default.asp
 [4]: http://pgfoundry.org/projects/oledb/
 [5]: http://pgfoundry.org/projects/psqlodbc/