---
title: Listing All Passwords Stored in Gnome Keyring
author: Michael Schurter
layout: post
date: 2008-10-31
url: /2008/10/30/listing-all-passwords-stored-in-gnome-keyring/
dsq_thread_id:
  - 463870799
categories:
  - Open Source
  - Python
  - Technology
tags:
  - 1337
  - gnome
  - gtk
  - Python

---
I was toying with writing my first desktop application in years and got distracted by how cool [Gnome Keyring][1] is. Of course storing and retrieving passwords is pretty mundane, so here&#8217;s a fun example that dumps all of the current user&#8217;s passwords:

<pre lang="python">#!/usr/bin/env python

import pygtk
pygtk.require('2.0')
import gtk # sets app name
import gnomekeyring

def hack():
    for keyring in gnomekeyring.list_keyring_names_sync():
        for id in gnomekeyring.list_item_ids_sync(keyring):
            item = gnomekeyring.item_get_info_sync(keyring, id)
            print '[%s] %s = %s' % (
                    keyring, item.get_display_name(), item.get_secret())
        else:
            if len(gnomekeyring.list_item_ids_sync(keyring)) == 0:
                print '[%s] --empty--' % keyring

if __name__ == '__main__':
    hack()
</pre>

Sample output with the interesting bits removed:

<pre>[default] Local password for user root = *******
[login] michael.schurter@Work = *******
[login] Google Account = *******
[login] Passphrase for wireless network 2WIRE939 = *******
[login] Unlock password for default keyring = *******
[login] schmichael@twitter.com = *******
[session] --empty--
</pre>

Its not meant to be any sort of real hacking tool. After all you can view all of this information via [Seahorse][2] anyway.

But what fun is a _GUI_ tool? 😉

 [1]: http://live.gnome.org/GnomeKeyring
 [2]: http://live.gnome.org/Seahorse