---
title: Fun with Django and modwsgi
author: Michael Schurter
layout: post
date: 2008-02-06
url: /2008/02/05/fun-with-django-and-modwsgi/
dsq_thread_id:
  - 463870650
categories:
  - Open Source
  - Python
  - Technology
tags:
  - apache
  - cherrypy
  - diy
  - django
  - dreamhost
  - fastcgi
  - modwsgi
  - mod_python
  - Python
  - wsgi

---
Today I deployed my first [Django][1] application for a client. Its yet-another-blog, so I&#8217;ll refrain from posting the code and cluttering up the django-\*blog\* namespace on Google Code. Before you roll your eyes and complain about why I didn&#8217;t use an existing solution, I think I have 2 somewhat valid reasons:

  1. The client actually needed a _sub_set of the features most blogs offer, so I wouldn&#8217;t really have anything to contribute back to an existing project.
  2. Blogs are one of the simplest content driven web applications in existence. Wikis are just a bit simpler perhaps. At any rate, creating a blog app is an excellent way to learn a framework.

**Python Deployment Decisions**

In the past I&#8217;ve used [CherryPy as my framework and a simple mod_proxy configuration to run the applications behind Apache][2]. [Django considers its built-in web server a development tool only][3], so I figured it was time to explore the myriad of Python web app deployment alternatives: [mod_python][4], [FastCGI][5], [modwsgi][6]. I&#8217;m sure there are many more, but I&#8217;d say those are the big 3.

I had tried to deploy Python web applications on DreamHost using FastCGI before and entered [the hell that is deploying Python web apps on shared hosts][7]. _So FastCGI wasn&#8217;t my first choice this time._

I had also tried mod_python for deploying [CherryPy][8] apps on my [Linode][9] before and for whatever reason just found [mod_proxy][10] to be _much_ easier to setup and manage.

I was kind of eager to try out modwsgi because its been getting a lot of attention lately, so I downloaded the source and compiled it on my [Debian][11] [Etch][12] server.

**Deploying a Django App via modwsgi**

modwsgi was quite easy to setup as long as you follow the instructions in their wiki for Django integration. I was hit by [bug #3762][13], but the modwsgi documentation got me through it. <small>(For what its worth the attached wsgi.patch also worked, but I don&#8217;t really want to run a patched version of Django.)</small>

One big problem I ran into was [sqlite3][14] gave me `OperationalError: unable to open database file` whenever I did anything that would write to the database. My database file was owned by `www-data` (the Apache process owner) and had the permissions `664`.

I switched to [PostgreSQL][15], ran [`syncdb`][16], and everything worked beautifully.

My wsgi script file /srv/spam/eggs/eggs.wsgi:

<pre lang="python">import os, sys
sys.path.append('/srv/spam')
sys.path.append('/srv/spam/eggs')
os.environ['DJANGO_SETTINGS_MODULE'] = 'eggs.wsgi_settings'

import django.core.handlers.wsgi

_application = django.core.handlers.wsgi.WSGIHandler()

def application(environ, start_response):
    environ['PATH_INFO'] = environ['SCRIPT_NAME'] + environ['PATH_INFO']
    return _application(environ, start_response)
</pre>

Note I use `wsgi_settings` instead of my usual settings file. wsgi_settings just imports my main settings file and changes some to their production values.

My Django application actually drops into the `/blog/` and `/accounts/` folders under a VirtualHost otherwise occupied by static files and some PHP scripts. modwsgi made this easy by putting this in my existing VirtualHost:

<pre lang="apache">WSGIScriptAliasMatch /(blog|accounts)/.* /srv/spam/eggs/eggs.wsgi

# A simple Alias directive handles my static files
Alias /static/ /srv/spam/eggs/static/
</pre>

**Bottom Line**

I highly recommend using modwsgi for deploying Python web applications. sqlite3 may work for you. In my case its probably best I use PostgreSQL for a number of reasons.

 [1]: http://www.djangoproject.com/
 [2]: http://michael.susens-schurter.com/blog/2007/08/16/deploying-cherrypy-on-apache-2-using-mod_proxy/
 [3]: http://www.djangoproject.com/documentation/django-admin/#runserver-optional-port-number-or-ipaddr-port
 [4]: http://www.modpython.org
 [5]: http://www.fastcgi.com/
 [6]: http://www.modwsgi.org
 [7]: http://www.al3x.net/2008/01/shared-hosting-is-ghetto.html
 [8]: http://www.cherrypy.org/
 [9]: http://www.linode.com/
 [10]: http://httpd.apache.org/docs/2.2/mod/mod_proxy.html
 [11]: http://www.debian.org/
 [12]: http://www.debian.org/releases/etch/
 [13]: http://code.djangoproject.com/ticket/3762
 [14]: http://docs.python.org/lib/module-sqlite3.html
 [15]: http://www.postgresql.org/
 [16]: http://www.djangoproject.com/documentation/django-admin/#syncdb