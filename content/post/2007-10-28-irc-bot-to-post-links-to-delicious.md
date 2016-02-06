---
title: IRC Bot to Post Links to Delicious
author: Michael Schurter
layout: post
date: 2007-10-28
url: /2007/10/28/irc-bot-to-post-links-to-delicious/
dsq_thread_id:
  - 463870602
categories:
  - Open Source
  - Python
  - Technology

---
I lurk in an IRC chatroom with some friends and throughout the course of a day a lot of links are posted.

I wanted to be able to catch up on the links without having to read through the entire channel backlog, so I hacked together a new module for [Phenny][1] (a Python IRC bot) which posted the links to a [Delicious][2] account. I subscribe to that account via Google Reader, and read through the latest Internet memes at my leisure. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

To use my little hack:

  1. Install [pydelicious][3]
  2. Install [Phenny][1]
  3. copy the following code into a new file: `modules/delicious.py` <pre lang="python">#!/usr/bin/env python
"""
delicious.py - Automatically post URLs to delicious
Author: Michael Schurter, http://michael.susens-schurter.com/
License: Public Domain
About: http://inamidst.com/phenny/
"""

import re
import pydelicious

r = re.compile(r'http\S*')

def f_delicious(self, origin, match, args):
  try:
    matches = r.findall(match.group())
    if matches:
      d = pydelicious.DeliciousAPI('DELICIOUS_USERNAME', 'DELICIOUS_PASSWORD')
      for url in matches:
        title = '%s: %s' % (origin.nick, match.group())
        if len(title) > 50:
          title = '%s...' % title[:50]
        d.posts_add(
          url=url,
          description=title,
          extended=match.group(),
          # Add custom tags below
          tags='oggbot oggbot-added-by:%s' % origin.nick
        )
  except:
    self.msg(origin.sender, 'Oops!  Missed that one.  Blame schmichael!')
f_delicious.rule = r'.*'
</pre>

  4. Fill in delicious account information in the obvious place.
  5. Start/Restart Phenny and watch posted links appear in delicious.</ul> 

There&#8217;s lots of room for improvement in the code, but it works for me!

<small>Sorry for poor tab spacing. I had vim configured for some Drupal hacking and forgot to switch back to 4-space tabs.</small>

 [1]: http://inamidst.com/phenny/
 [2]: http://del.icio.us/
 [3]: http://code.google.com/p/pydelicious/