---
title: Thank God for PHP_Compat
author: Michael Schurter
layout: post
date: 2005-08-05
url: /2005/08/05/thank-god-for-php_compat/
dsq_thread_id:
  - 1359952315
categories:
  - PHP

---
So I was hacking on a little PHP project to parse JULIE Ticket e-mails. I [mentioned it before][1], and while I&#8217;m still having fun with simple string parsing functions, being able to use [PHP5&#8217;s `file_put_contents()` function][2] in PHP4 would be nice.

Thank God for [PHP_Compat][3]. Here&#8217;s how easy it is to use `file_put_contents()` in PHP4:

  1. In a console window: `pear install php_compat`
  2. In PHP:
  
    `require_once(PHP/Compat/Function/file_put_contents.php');<br />
file_put_contents($filename, $contents);`

And most importantly, it worked perfectly out of the box.

 [1]: http://blogs.synthesyssolutions.com/michael/2005/08/01/cs210-work/
 [2]: http://us2.php.net/manual/en/function.file-put-contents.php
 [3]: http://pear.php.net/package/PHP_Compat