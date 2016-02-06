---
title: mDNS crashes Samba
author: Michael Schurter
layout: post
date: 2006-11-29
url: /2006/11/29/mdns-crashes-samba/
dsq_thread_id:
  - 480134010
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
Wow. This was a weird one that ended causing me to use my feeble knowledge of _gdb_ figure out whats going on.

I&#8217;ve been messing around with the best way to integrate my Debian GNU/Linux desktop with the Active Directory network at work. Some recommended that I re-run the _net ads join_ command, but I kept getting a **Segmentation fault** error after entering my password!

A few minutes of toying with _gdb &#8211;args net ads join_ and the _bt_ (backtrace) command showed me the crash was in **libnss_mdns**! libnss_mdns is the multicast DNS name resolution service used by Avahi. mDNS uses the .local domain and our Active Directory uses the <span style="font-style: italic">tremont.<span style="font-weight: bold">local</span></span> domain name, so I wonder if there&#8217;s some sort of conflict&#8230;
  
After removing all mention of **mdns** and **minimal_mdns** from my **/etc/nsswitch.conf** file, _net ads join_ ran perfectly.

Here&#8217;s the backtrace for anyone interested (or googling):

<p style="text-align: left">
  #0 0x0816e15d in timeval_add ()<br /> #1 0xb791e76b in avahi_resolve_address () from /usr/lib/libnss_mdns.so.2<br /> #2 0xb791ed09 in mdns_query_ipv4 () from /usr/lib/libnss_mdns.so.2<br /> #3 0xb791c979 in _nss_mdns_gethostbyaddr_r () from /usr/lib/libnss_mdns.so.2<br /> #4 0xb7cb6389 in gethostbyaddr_r () from /lib/tls/i686/cmov/libc.so.6<br /> #5 0xb7cbeaac in getnameinfo () from /lib/tls/i686/cmov/libc.so.6<br /> #6 0xb7da9c3a in ldap_pvt_get_hname () from /usr/lib/libldap_r.so.2<br /> #7 0xb7da5007 in ldap_host_connected_to () from /usr/lib/libldap_r.so.2<br /> #8 0xb7d91060 in ldap_int_open_connection () from /usr/lib/libldap_r.so.2<br /> #9 0xb7da3503 in ldap_new_connection () from /usr/lib/libldap_r.so.2<br /> #10 0xb7d90ef1 in ldap_open_defconn () from /usr/lib/libldap_r.so.2<br /> #11 0xb7d91776 in ldap_open () from /usr/lib/libldap_r.so.2<br /> #12 0x081cc341 in ldap_open_with_timeout ()<br /> #13 0x081cc41f in ads_connect ()<br /> #14 0x0807b9b1 in net_ads_check_our_domain ()<br /> #15 0x0807d4bf in net_ads_join ()<br /> #16 0x0807afa9 in net_ads ()<br /> #17 0x0807adea in main ()
</p>

I don&#8217;t even know **where to submit a bug report** since (at least) 3 separate projects are referenced in the backtrace: [Samba][1], [OpenLDAP][2] (libldap), and [Avahi][3]/libnss_mdns. Anyone able to enlighten me?

**Update:**Â  Gerald (Jerry) Carter from the Samba Team [told someone with a similar experience to report the bug to the Avahi team][4].Â  [So I did][5].

 [1]: http://samba.org
 [2]: http://www.openldap.org/
 [3]: http://avahi.org/
 [4]: http://lists.samba.org/archive/samba/2006-July/123102.html
 [5]: http://avahi.org/ticket/78