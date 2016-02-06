---
title: 'SchoolWorks on Linux: Part 1 of Many'
author: Michael Schurter
layout: post
date: 2006-09-07
url: /2006/09/06/schoolworks-on-linux-part-1-of-many/
dsq_thread_id:
  - 463870171
categories:
  - GNU/Linux
  - Mono/.Net
  - Open Source
  - PostgreSQL
  - SQL
  - Technology
tags:
  - Synthesys

---
Now that [SchoolWorks][1] has officially been released, I guess I can begin posting about my attempts to get it running on Linux.

First of all SchoolWorks is school administration software (or [SIS][2]) built using:

  * [ASP.NET][3] 2.0 (in Windows using [Microsoft Visual Studio][4] 2005)
  * [PostgreSQL][5] (thanks to [Npgsql][6])
  * Crystal Reports (great for report designers, [abhorrent for developers][7])

We also used the following support tools:

  * [Bugzilla][8]
  * [Subversion][9] and [TortoiseSVN][10]
  * [PgAdmin III][11]

While Visual Studio and ASP.NET can be frustrating at times, the only part of SchoolWorks that I avoid like the plague is working with Crystal Reports.

Recently I&#8217;ve been trying to build SchoolWorks using [Mono][12] on Linux. I&#8217;ve successfully [built Mono][12] (libgdiplus + mono + mcs + xsp) on my personal [Debian Etch][13], but I haven&#8217;t gotten much of SchoolWorks to compile yet.

The first missing feature was [Decimal.TryParse][14] which we use a lot in SchoolWorks. [I submitted (my very first!) patch to the mono-devel mailing list in hopes of getting support for Decimal.TryParse added][15].

I&#8217;ll try to keep posting my progress as it should be interesting to SchoolWorks users as well as .NET/Mono developers.

 [1]: http://www.schoolworksinc.com/
 [2]: http://en.wikipedia.org/wiki/Student_information_system
 [3]: http://msdn.microsoft.com/asp.net/
 [4]: http://msdn.microsoft.com/vstudio/
 [5]: http://www.postgresql.org/
 [6]: http://pgfoundry.org/projects/npgsql
 [7]: http://blogs.synthesyssolutions.com/michael/2006/08/23/never-use-crystal-reports-again/
 [8]: http://www.bugzilla.org/
 [9]: http://subversion.tigris.org/
 [10]: http://tortoisesvn.net/
 [11]: http://www.pgadmin.org/
 [12]: http://www.mono-project.com/
 [13]: http://www.debian.org/releases/etch/
 [14]: http://msdn2.microsoft.com/en-us/library/system.decimal.tryparse.aspx
 [15]: http://lists.ximian.com/pipermail/mono-devel-list/2006-September/020302.html