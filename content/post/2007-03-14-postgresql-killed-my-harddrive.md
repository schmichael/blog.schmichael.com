---
title: PostgreSQL Killed My Harddrive
author: Michael Schurter
layout: post
date: 2007-03-14
url: /2007/03/14/postgresql-killed-my-harddrive/
dsq_thread_id:
  - 690421340
categories:
  - PostgreSQL
  - SQL
  - Technology

---
The harddrive died in the server that dumps our firewall&#8217;s syslog output into a nice [PostgreSQL][1] database for easy reporting. PostgreSQL didn&#8217;t do anything evil in order to kill the drive, but because [it syncs data to the harddrive for safety][2], it kept my ancient server&#8217;s harddrive spinning 24/7.

I should mention this was my fault. I really should have [turned fsync off][3] to let the server cache the trickle of ICMP packets that keep our firewall awake all night. Instead the old Quantum Fireball Plus LM harddrive wrote every byte right as it came in.

Luckily the harddrive still worked enough that I could attach it to another computer via a IDE-USB adapter and copy off any data I wanted to keep.

Below are the SMART statistics for the drive as collected by [smartmontools][4] and [munin][5]. As I was able to retrieve data off the disk, I would say SMART did its job even if it didn&#8217;t give me much warning.

[![moodletremontlocal-smart_hda-day.png][6]][7]
  
[![moodletremontlocal-smart_hda-month.png][8]][9]

 [1]: http://www.postgresql.org
 [2]: http://developer.postgresql.org/pgdocs/postgres/runtime-config-wal.html
 [3]: http://www.postgresql.org/docs/8.1/interactive/runtime-config-wal.html
 [4]: http://smartmontools.sourceforge.net/
 [5]: http://munin.projects.linpro.no/
 [6]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/03/moodletremontlocal-smart_hda-day.png
 [7]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/03/moodletremontlocal-smart_hda-day.png "moodletremontlocal-smart_hda-day.png"
 [8]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/03/moodletremontlocal-smart_hda-month.png
 [9]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/03/moodletremontlocal-smart_hda-month.png "moodletremontlocal-smart_hda-month.png"