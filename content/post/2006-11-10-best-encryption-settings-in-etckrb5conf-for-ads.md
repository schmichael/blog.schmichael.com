---
title: Best encryption settings in /etc/krb5.conf for ADS
author: Michael Schurter
layout: post
date: 2006-11-10
url: /2006/11/10/best-encryption-settings-in-etckrb5conf-for-ads/
dsq_thread_id:
  - 483528118
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology

---
As you can tell from my previous posts, I&#8217;m fighting trying to get the ideal Linux-in-a-Windows-environment setup. My original encryption settings in /etc/krb5.conf seem to fail for some users when communicating with the KDC which in this case is a Microsoft Windows 2000 ADS (ActiveDirectory Server).

Here&#8217;s my new and improved /etc/krb5.conf file:

<pre>[libdefaults]
default_realm = TREMONT.LOCAL

# The following krb5.conf variables are only for MIT Kerberos.
krb4_config = /etc/krb.conf
krb4_realms = /etc/krb.realms
kdc_timesync = 1
ccache_type = 4
forwardable = true
proxiable = true

## For Windows 2000 ADS
default_tgs_enctypes = rc4-hmac des-cbc-crc des-cbc-md5
default_tkt_enctypes = rc4-hmac des-cbc-crc des-cbc-md5
permitted_enctypes = rc4-hmac des-cbc-crc des-cbc-md5

[realms]
TREMONT.LOCAL = {
kdc = thsdc1
kdc = thsdc2
admin_server = thsdc1
}
[domain_realm]
.tremont.local = TREMONT.LOCAL
.tremont.com = TREMONT.LOCAL
[login]
krb4_convert = true
krb4_get_tickets = false</pre>

  * Some user accounts would not work until I added the **rc4-hmac** encryption type which evidently is **Window&#8217;s default**.
  * I&#8217;m not sure about the **.tremont.com** domain name mapping, but I added it because our Exchange server thinks .tremont.com is somehow related to .tremont.local. Thats something that probably warrants looking into on the server.
  * **thsdc2** is a backup ADS.

<small>Still looking for some easy way to post code/config files in WordPress 2.x. Even though it properly recognizes my <em>pre</em> tags it still strips out my leading tabs and spaces. Please <a href="mailto:michael@susens-schurter.com">let me know</a> if you have a solution</small>