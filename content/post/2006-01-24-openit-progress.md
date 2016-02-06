---
title: OpenIT Progress
author: Michael Schurter
layout: post
date: 2006-01-25
url: /2006/01/24/openit-progress/
dsq_thread_id:
  - 554714958
categories:
  - PHP
  - PostgreSQL
  - SQL
  - Technology
tags:
  - OpenIT
  - Synthesys

---
I&#8217;ve been keeping up a good pace of bug fixing in [OpenIT][1] thanks to user bug reports. I&#8217;m really getting bitter about using [MySQL][2] 4.0, especially after we&#8217;ve started using [PostgreSQL][3] for a new project at Synthesys.

[Views][4]? [Foreign Key Constraints][5]? [Cascading UPDATEs and DELETEs][6]? I&#8217;ve had to implement these in PHP! Lord have mercy on my soul. While I appreciate how easy MySQL is to install and use, after using PostgreSQL for just a short while I&#8217;m ready to drop MySQL and never look back.

 [1]: https://sourceforge.net/projects/openit
 [2]: http://www.mysql.com
 [3]: http://www.postgresql.org
 [4]: http://www.postgresql.org/docs/8.1/interactive/tutorial-views.html
 [5]: http://www.postgresql.org/docs/8.1/interactive/tutorial-fk.html
 [6]: http://www.postgresql.org/docs/8.1/interactive/ddl-constraints.html#DDL-CONSTRAINTS-FK