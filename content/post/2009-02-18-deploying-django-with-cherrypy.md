---
title: (Yet Another) Deploying Django with CherryPy Script
author: Michael Schurter
layout: post
date: 2009-02-18
url: /2009/02/18/deploying-django-with-cherrypy/
dsq_thread_id:
  - 463870863
categories:
  - GNU/Linux
  - Open Source
  - Python
  - Technology
tags:
  - cherrypy
  - django
  - Python

---
Recently I deployed a [Django][1] project on an OSX server. I foolishly thought this would be as easy as on Linux until I ran into the mess that is _x86_64_ Apache + [mod_wsgi][2]* + Django + psycopg2 + _i386_ PostgreSQL. After wasting far too much time googling and recompiling various bits trying to get everything happy, I followed [Eric Florenzano&#8217;s post][3] on deploying Django using [CherryPy][4]&#8216;s** [wsgiserver][5].

Here&#8217;s my lightly modified version of Eric&#8217;s script:

<pre lang="python">import wsgiserver
import sys
import os
import django.core.handlers.wsgi

if __name__ == "__main__":
    # Setup paths - a bit hackish, but works for me.
    # Assumes an absolute path is stored in &lt;project>.local_settings.ROOT
    sys.path.append(os.path.realpath(os.path.dirname(__file__)))
    from foo.local_settings import ROOT
    sys.path.append(ROOT)

    # Startup Django
    os.environ['DJANGO_SETTINGS_MODULE'] = 'foo.settings'
    server = wsgiserver.CherryPyWSGIServer(
        ('0.0.0.0', 8888),  # Use '127.0.0.1' to only bind to the localhost
        django.core.handlers.wsgi.WSGIHandler()
    )
    try:
        server.start()
    except KeyboardInterrupt:
        print 'Stopping'
        server.stop()
</pre>

I also went with the latest stable version of CherryPy&#8217;s wsgiserver instead of checking out trunk like Eric&#8217;s post suggested.

Then I just enabled `mod_proxy` in Apache and setup the following VirtualHost:

<pre lang="apache">&lt;Proxy *>
    Order allow,deny
    Allow from all
&lt;/Proxy>
&lt;Location "/">
    ProxyPass http://127.0.0.1:8888/
    ProxyPassReverse http://127.0.0.1:8888/
&lt;/Location>
</pre>

If you&#8217;re cool you&#8217;ll write some sort of system specific script to launch your web app on boot. In a pinch, you can always use a crontab:

<pre lang="bash">@reboot /usr/bin/python /path/to/app.py &#038;
</pre>

YMMV 😉

<small><br /> * To mod_wsgi&#8217;s credit, it took about 10 seconds to compile, generated a Universal binary, and in general Just Worked.</p> 

<p>
  ** I&#8217;m already a CherryPy fan thanks to <a href="http://www.dowski.com/">dowski</a>, so it wasn&#8217;t a hard decision.<br /> </small>
</p>

 [1]: http://www.djangoproject.com/
 [2]: http://www.modwsgi.org/
 [3]: http://www.eflorenzano.com/blog/post/hosting-django-site-pure-python/
 [4]: http://www.cherrypy.org/
 [5]: http://www.cherrypy.org/wiki/CherryPyDownload#StandaloneWSGIserver