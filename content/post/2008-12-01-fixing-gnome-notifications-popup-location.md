---
title: Fixing Gnome Notification’s Popup Location
author: Michael Schurter
layout: post
date: 2008-12-02
url: /2008/12/01/fixing-gnome-notifications-popup-location/
dsq_thread_id:
  - 463870815
categories:
  - GNU/Linux
  - Technology
tags:
  - debian
  - gnome
  - notifications
  - Python

---
Gnome notifications popup in the lower left corner of your desktop by default* which constantly annoys me. I usually have a terminal open in the lower left corner, and having my work covered by notifications is quite annoying.

Luckily the fix is easy:

  1. Open Applications > System Tools > Configuration Editor**
  2. Navigate to `apps` > `notification-daemon`
  3. Edit the `popup_location` to be something less annoying. I prefer **`top_right`**.
  4. Close Configuration Editor. Changes will take effect next time you login _or_ just restart the notification-daemon: <pre lang="bash">~$ killall notification-daemon
~$ /usr/lib/notification-daemon/notification-daemon &#038;
</pre>

Note that the notifications will actually show up over the top of your panel which seems a bit strange. However, I&#8217;d rather the notification covered the panel than take up any more precious application space than is necessary.

Luckily you can easily test notifications if you have Python and python-notify installed:

<pre lang="python">>>> import pynotify
>>> pynotify.init('foo')
True
>>> pynotify.Notification('foo', 'bar').show()
True
</pre>

![Notification in the upper right.][1]

* at least on Gnome 2.22.3 on Debian Sid with notification-daemon 0.3.7-1+b1
  
** aka [gconf-editor][2] from the [gconf-editor package][3] which should be installed with Gnome.

 [1]: /files/notification-top_right.png
 [2]: http://projects.gnome.org/gconf/
 [3]: http://packages.debian.org/search?keywords=gconf-editor&searchon=names&suite=all&section=all&sourceid=mozilla-search