---
title: Common Django Typo in URLconf
author: Michael Schurter
layout: post
date: 2008-03-10
url: /2008/03/10/common-django-typo-in-urlconf/
dsq_thread_id:
  - 463870668
categories:
  - Open Source
  - Python
  - Technology
tags:
  - django
  - exception
  - Python
  - typo

---
If you&#8217;re hacking Django and get this&#8230;

`ImproperlyConfigured: Error while importing URLconf 'proj.app.urls': 'tuple' object is not callable`

&#8230;you&#8217;re probably [missing a comma in your URL configuration as Rajesh Dhawan pointed out][1].

<small>Django pros can move along, I know you never make typos. 😉</small>

 [1]: http://groups.google.com/group/django-users/browse_thread/thread/517ea56bece07c86?hide_quotes=no#msg_f6f321e7997ce992