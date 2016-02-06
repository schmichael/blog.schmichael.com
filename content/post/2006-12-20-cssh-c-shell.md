---
title: 'cssh: C# Shell'
author: Michael Schurter
layout: post
date: 2006-12-20
url: /2006/12/20/cssh-c-shell/
dsq_thread_id:
  - 464710417
categories:
  - GNU/Linux
  - Mono/.Net
  - Open Source
  - PHP
  - Technology

---
The other day I found myself writing a shell script in PHP because I refuse to learn bash&#8217;s archaic syntax.Â  I&#8217;m actually a lot happier with PHP as a shell scripting language than a web application language.Â  However, I&#8217;ve always wanted a scripting language with the power of Mono/.NET.

So yesterday I quickly threw together _cssh_: C# Shell.Â  You can&#8217;t use it as a real shell like bash, but it does allow you to write quick little C# programs that can be run like a script.

Basically the shebang (#!) tells your shell to run your script via cssh.Â  cssh then strips out the shebang line, prepends a Class and a Method declaration, appends a _return 0;_ as well as a couple closing brackets (}), and executes it in memory using Microsoft.CSharp namespace and Reflection.

In all it took about 60 lines of code to write.Â  You can [**download** a zip file with the source and a binary][1] if you&#8217;re interested.Â  It should compile and execute just fine under both Mono and Windows/.NET, although Windows lacks shebang script support.

While this was an interesting exercise, I&#8217;m not sure its worth pursuing.Â  C# isn&#8217;t a scripting language, so to make it really useful you&#8217;d want to make some language modifications.Â  I think I&#8217;m going to take a look at [boo][2] or [python][3] instead of continuing to develop cssh.Â  Although I do love my semicolons&#8230;

 [1]: http://michael.susens-schurter.com/code/cssh.zip
 [2]: http://www.mono-project.com/Boo
 [3]: http://www.python.org/