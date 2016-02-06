---
title: register_globals is evil
author: Michael Schurter
layout: post
date: 2005-08-11
url: /2005/08/11/register_globals-is-evil/
dsq_thread_id:
  - 580166281
categories:
  - PHP

---
Disclaimer: I am not a PHP security expert. The open source PHP web application I develop, [OpenIT][1] isn&#8217;t exactly a poster child for best security practices.

I enjoyed reading [Stefan Esser&#8217;s blog: register_globals is not evil][2], and I agree with many of the things he wrote. In fact the main problem I have with his article is the title. A more accurate (but less fun) title would be &#8220;register_globals is evil, but plan for it.&#8221;

In my humble opinion [register_globals][3] is one of the worst language &#8220;features&#8221; PHP has. Under no circumstances should it be used, and every night when I say my prayers I ask [God][4] to deprecate it in future versions of PHP. The ability for users to override/create arbitrary variables in a PHP application is frightening, and &#8220;C does it too!&#8221; is never appropriate to say in a discussion about security.

Stefan has some excellent points about how assuming register\_globals is off in your web apps is the real security threat. As long as the evil that is register\_globals exists in this world, PHP applications will have to contiue wasting their time protecting against it.

Unfortunately, [OpenIT][5] is one of these offending applications&#8230; I just committed a new .htaccess file to turn register_globals off, but this probably isn&#8217;t enough.

 [1]: http://openit.sourceforge.net/
 [2]: http://blog.php-security.org/archives/3-register_globals-is-not-evil.html
 [3]: http://us2.php.net/register_globals
 [4]: http://www.zend.com/
 [5]: http://cvs.sourceforge.net/viewcvs.py/openit/OpenIT/.htaccess?rev=1.4&view=auto