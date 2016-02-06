---
title: Recipe for a Transparent Linux Firewall and CherryPy Control Panel
author: Michael Schurter
layout: post
date: 2007-11-06
url: /2007/11/06/recipe-for-a-transparent-linux-firewall-and-cherrypy-control-panel/
dsq_thread_id:
  - 463870616
categories:
  - GNU/Linux
  - IT
  - Python
  - Technology
tags:
  - cherrypy
  - debian etch
  - iptables

---
<div style="float: right; padding: 10px;">
  <a href="http://michael.susens-schurter.com/files/firewalladmin.png"><img alt="firewalladmin screenshot" src="http://michael.susens-schurter.com/files/firewalladmin-small.png" /></a>
</div>

At my previous job I built a transparent firewall with the help of a student. He hacked up some iptables scripts, and I hacked up a CherryPy application to control the firewall. It turned out to be pretty handy, so I&#8217;m finally getting around to posting it somewhere&#8230;

**Recipe:** A transparent firewall to block certain IP addresses and a nice web based control panel to edit the blacklist.

**Ingredients:**

  * Old computer (preferably a PIII) with 3 NICs
  * [Debian Etch][1] (or your Linux flavor of choice)
  * Packages: [iptables][2], [bridge-utils][3], [Python][4], [setuptools][5], CherryPy 3 (use easy\_install), Genshi (use easy\_install), [Python-ADNS][6], [SQLObject][7]
  * [firewall-admin.tar.gz][8] &#8211; my exceedingly creatively named firewall administration CherryPy web app

**Directions:**

  1. Extract firewall-admin.tar.gz and change to the base directory. By default its setup to be in /srv/firewall-admin
  2. If you didn&#8217;t extract to `/srv/firewall-admin`, edit etc/rc.local and _basedir_ in `firewalladmin.config` to reflect the current directory.
  3. By default `firewalladmin/lib/bridge.py` [bridges][9] _eth1_ and _eth2_, and _eth0_ should be attached to your LAN to access SSH and the web control panel.
  4. Edit firewalladmin.config to run on the IP address assigned to your administrative NIC and remember what port its set to run on.
  5. Add the commands from `etc/rc.local` to your system&#8217;s existing `/etc/rc.local` script. This will start the transparent firewall and web control panel on boot.
  6. Next you&#8217;ll need to setup the database. Edit line 28 in `firewalladmin/model.py` to set a default password and then run `createdb.py`
  7. You&#8217;re now ready to start the firewall and control panel simply by running `sudo etc/rc.local` (see _Caveats_ below). You can always test out just the web interface by running `start-firewalladmin.py`
  8. Browse to the web interface using the IP and Port setup in step 4, login using the username and password setup in step 6, and start configuring your transparent firewall!

The firewall allows creating multiple blacklists (aka Categories) which can be edited/paused/deleted individually. It has has _allow lists_ (aka Whitelists) which can be used to allow specific internal IPs access to specific sites that might otherwise be blocked by a blacklist.

**Important:** When a user visits a blocked site they are redirected to the IP and Port specified on line 10 of `firewalladmin/lib/iptables.py`. We setup Apache to listen on that port and serve up a generic _You&#8217;ve been blocked_ page, but you could be even more clever. You&#8217;ll need a `.htaccess` file like the following to properly map all blocked traffic to your block page:

<pre lang="htaccess">RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.html [L,QSA]
</pre>

**Caveats**

  * All scripts as well as the web control panel are **executed as root**. This setup should only be run on dedicated hardware and not on a server with other services.
  * No test suite. Mea culpa.
  * Little to no error handling. You&#8217;ve been warned. 😉
  * Basically this is a quick hack and should not be used in the same way you use tested and maintained software. YMMV

This little setup has proved very useful at the school for augmenting their existing content filtering system, and all web traffic passes through it without trouble. An old PIII can run a 3,000 domain blacklist at wirespeed on a 10 Mbps link while using less than 10% of the CPU.

 [1]: http://www.debian.org/releases/etch/
 [2]: http://packages.debian.org/etch/iptables
 [3]: http://packages.debian.org/etch/bridge-utils
 [4]: http://packages.debian.org/etch/python/python
 [5]: http://packages.debian.org/etch/python/python-setuptools
 [6]: http://packages.debian.org/etch/python/python-adns
 [7]: http://packages.debian.org/etch/python/python-sqlobject
 [8]: http://michael.susens-schurter.com/code/firewall-admin.tar.gz
 [9]: http://www.linux-foundation.org/en/Net:Bridge