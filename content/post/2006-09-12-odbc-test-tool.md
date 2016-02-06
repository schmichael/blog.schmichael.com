---
title: ODBC Test Tool
author: Michael Schurter
layout: post
date: 2006-09-12
url: /2006/09/12/odbc-test-tool/
dsq_thread_id:
  - 465467493
categories:
  - Mono/.Net
  - SQL
  - Technology

---
Today I find myself once again fighting Crystal Reports. It claims that it can&#8217;t connect to the ODBC datasource I created for it since it can&#8217;t use Npgsql. Just to prove it wrong I quick hacked together an ODBC Test Tool in [SharpDevelop][1]. Sure enough, the ODBC connection works just fine.

[Here&#8217;s a zip of ODBCTestTool][2] which contains the source code and compiled executables under the _bin_ directory. It requires .NET 2.0, and I doubt it runs on Mono since it uses ODBC.

Oh and I didn&#8217;t include any license information, so I guess its public domain. Have fun.

 [1]: http://www.icsharpcode.net/OpenSource/SD/
 [2]: http://blogs.synthesyssolutions.com/michael/wp-content/uploads/2006/09/ODBCTestTool-0.1.zip