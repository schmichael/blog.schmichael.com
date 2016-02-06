---
title: Deploying CherryPy on Apache 2 using mod_proxy
author: Michael Schurter
layout: post
date: 2007-08-16
url: /2007/08/16/deploying-cherrypy-on-apache-2-using-mod_proxy/
dsq_thread_id:
  - 463870518
categories:
  - GNU/Linux
  - Open Source
  - PHP
  - Python
  - Technology

---
**Background**

I&#8217;ve been trying to move away from PHP to [Python][1] for web applications. I tried [Django][2] and [TurboGears,][3] but I settled upon the more basic [CherryPy][4] framework. It helped that my friend [Christian][5] is active in the CherryPy community and promised to answer all of my stupid questions (thanks Christian!).

Regardless of which framework I had chosen though, they all have a significant architectural difference from PHP:

  * PHP is a _scripting language_.
  * Django, TurboGears, CherryPy, etc. are _application servers_.

Technically Python is a scripting language and PHP+Apache could be called an application server, so I should explain:

  * PHP web applications are executed from start to finish for each web request.
  * The Python frameworks all run as a daemon and requests are processed based on object and method mappings.

<small>Still probably a gross oversimplification, but for the sake of brevity lets move on!</small>

The reason I mention these fundamental differences is because they **completely change how you deploy your web applications.** _PHP scripts can be FTPed_ (via SSH/SSL/TLS of course!) to a web accessible directory and instantly accessed. _Python web applications must be started_ and somehow integrated with your existing web server (Apache 2 in my case).

**The Problem**

_So how do you deploy CherryPy applications and have them play nice with Apache 2?_

**One Solution: Using [mod_proxy][6]**

_Warning:_ These instructions are for [_Debian Etch_][7], but the principles should be fairly universal.

Example domain: `www.example.com`
  
Example CherryPy URL: `http://www.example.com/webapp/`
  
Example CherryPy Root Object: `WebApp()`
  
Example CherryPy Configuration File: `webapp.config`

  1. Install Apache 2 (if you don&#8217;t use PHP, feel free to choose a MPM other than prefork) and Python
  2. Install python-setuptools if you haven&#8217;t already:
  
    `sudo apt-get install python-setuptools`
  3. Install CherryPy via _easy_install_ to get the latest stable version:
  
    `sudo easy_install cherrypy`
  4. Edit your CherryPy applications&#8217; config file (webapp.config in this example) to include the following lines:
  
    `server.socket_port = 6464<br />
server.socket_host = "127.0.0.1"`
  5. To start your web application you should have a line similar to:
  
    <code style="text-align: left;">cherrypy.quickstart(WebApp(), '/webapp', 'webapp.config')</code>
  6. Start your application as a background process. I usually use a command like this:
  
    <code style="text-align: left;">python start-webapp.py &gt; stdout.log &</code>
  7. If you have lynx or links installed you can test your web application:
  
    <code style="text-align: left;">lynx http://127.0.01:6464/webapp/</code>
  8. Enable mod_proxy for Apache 2:
  
    <code style="text-align: left;">sudo a2enmod proxy_http</code>
  9. Add the following to the **Apache virtual host configuration for _www.example.com_** (for example: /etc/apache2/sites-enabled/000-default or /etc/apache2/sites-enabled/www.example.com):
  
    <code style="text-align: left">ProxyPreserveHost on&lt;br />
&lt;Proxy *&gt;&lt;br />
&nbsp;&nbsp;Order allow,deny&lt;br />
&nbsp;&nbsp;Allow from all&lt;br />
&lt;/Proxy&gt;&lt;br />
ProxyPass /webapp/ http://127.0.0.1:6464/webapp/&lt;br />
ProxyPassReverse /webapp/ http://127.0.0.1:6464/webapp/</code>
 10. Restart Apache 2 using the following command:
  
    `sudo /etc/init.d/apache2 force-reload`

Go to http://www.example.com/webapp to see if it works!

**Caveats and Tips
  
** 

  * Be careful using **absolute URLs** (especially in **redirects**!) in your web application.
  * To make sure your web application **always starts at boot**, add this line to your _crontab_:
  
    <code style="text-align: left">@reboot /usr/bin/python /path/to/start-webapp.py &gt; /path/to/stdout.log &</code>

**Other Solutions**

Using mod_proxy is neither the only way to deploy CherryPy web applications nor the best for all deployment scenarios. Once I have a bit more experience I&#8217;d love to post a side-by-side comparison, but for now your probably best off reading [CherryPy&#8217;s wiki article on the subject][8].

 [1]: http://python.org/
 [2]: http://www.djangoproject.com/
 [3]: http://turbogears.org/
 [4]: http://cherrypy.org/
 [5]: http://dowski.com/
 [6]: http://httpd.apache.org/docs/2.2/mod/mod_proxy.html
 [7]: http://www.debian.org/releases/etch/
 [8]: http://tools.cherrypy.org/wiki/BehindApache