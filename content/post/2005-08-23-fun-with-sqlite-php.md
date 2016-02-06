---
title: Fun with SQLite + PHP
author: Michael Schurter
layout: post
date: 2005-08-23
url: /2005/08/23/fun-with-sqlite-php/
dsq_thread_id:
  - 463869760
categories:
  - PHP
  - SQL
tags:
  - OpenIT

---
My poor little OpenIT development box which runs on a whopping 48 MB of RAM has been running unusually slow, and I think its due to upgrading from MySQL 4.0 to 4.1. That&#8217;s really the only thing thats changed on it, and MySQL is definitely gobbling up more than its fair share of memory.

So I thought I&#8217;d give [SQLite][1] a try. `pear install sqlite` resulted in `phpize failed`, so I did what any true Slackware user would do: compile it from scratch. After the usual configure, make, make install, all I had to do was add `extension=sqlite.so` to my php.ini to finish setting up SQLite in PHP.

Next up: setting up OpenIT to use SQLite. Luckily the [PEAR DB documentation][2] provided an example DSN for SQLite databases. However, that caused an error when PHP tried to parse the settings.ini file. Come to [find out][3], `parse_ini_file()` needs non-alphanumeric values to be double quoted! `tools/setup.php` failed when trying to setup the first (Campuses) table.

Long story short I created a custom PHP script and SQL script to build a SQLite database. I can now login to OpenIT, but inserts give me an unknown database error. I may keep trying to get it work because OpenIT appears to run much much faster using SQLite on this ancient computer.

 [1]: http://www.sqlite.org/
 [2]: http://pear.php.net/manual/en/package.database.db.intro-dsn.php
 [3]: http://us3.php.net/manual/en/function.parse-ini-file.php