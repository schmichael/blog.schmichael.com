---
title: Authenticating Against Active Directory in Linux
author: Michael Schurter
layout: post
date: 2006-11-07
url: /2006/11/07/authenticating-against-active-directory-in-linux/
dsq_thread_id:
  - 463870237
categories:
  - GNU/Linux
  - Open Source

---
I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
```I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
``` 
  
<span style="font-weight: bold">/etc/pam.d/common-account</span>
  
````I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
```I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
``` 
  
<span style="font-weight: bold">/etc/pam.d/common-account</span>
  
```` 
  
<span style="font-weight: bold">/etc/pam.d/common-session</span>
  
`````I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
```I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
``` 
  
<span style="font-weight: bold">/etc/pam.d/common-account</span>
  
````I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
```I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
``I finally got it. After about 5 hours of working on it, I&#8217;ve finally gotten **Linux to authenticate against Active Directory on a Windows 2000 Server**. I want to post how I have it configured because it seems like most documentation only takes you halfway.
  
Software used: [<span style="font-weight: bold">Debian</span> Etch][1], [<span style="font-weight: bold">Samba</span> 3.0.23c with <span style="font-weight: bold">Winbind</span> and pam_winbind][2], and [<span style="font-weight: bold">MIT Kerberos</span> with pam_libkrb5][3].

The first step after getting the prerequisite software installed is to <span style="font-weight: bold">join the domain</span>. Luckily Samba has excellent documentation on how to join an Active Directory Domain. Specifically <span class="sect2"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#id2574601">On-the-Fly Creation of Machine Trust Accounts</a> and </span><span class="sect1"><a href="http://www.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member">Samba ADS Domain Membership</a>.</span>

The next step is to hook Linux&#8217;s authentication ([PAM][4]) into Active Directory. Here are the relevant bits of my configuration files:

<span style="font-weight: bold">NOTE:</span> In the following examples <span style="font-weight: bold">TREMONT</span> is the domain, <span style="font-weight: bold">TREMONT.LOCAL</span> is the realm, and <span style="font-weight: bold">thsdc1</span> is the Windows 2000 ADS (sometimes referred to as a PDC or Primary Domain Controller).

<span style="font-weight: bold">/etc/samba/smb.conf</span> (relevant bits only)

`[global]<br />
# Domain workgroup = Tremont realm = TREMONT.LOCAL security = ADS add machine script = /usr/sbin/useradd -d /var/lib/nobody -g 100 -s /bin/false -M %u<br />
encrypt passwords = true<br />
## Commented the following out, but I don't know if its necessary<br />
# passdb backend = tdbsam<br />
obey pam restrictions = yes<br />
idmap uid = 10000-20000<br />
idmap gid = 10000-20000<br />
template shell = /bin/bash<br />
# Note: I do *not* use the separator username format: Domain\User<br />
#winbind separator = '\'<br />
# The following allows users to login with just Username<br />
winbind use default domain = yes<br />
winbind enum users = yes<br />
winbind enum groups = ye template homedir = /home/%D/%U`

<span style="font-weight: bold">/etc/krb5.conf</span> (from the <span style="font-style: italic">krb5-config</span> package)
  
`` 
  
<span style="font-weight: bold">/etc/pam.d/common-auth</span>
  
``` 
  
<span style="font-weight: bold">/etc/pam.d/common-account</span>
  
```` 
  
<span style="font-weight: bold">/etc/pam.d/common-session</span>
  
````` 

  * <span style="font-weight: bold">Note 1:</span> Once you&#8217;re satisfied with your setup, remove &#8220;<span style="font-style: italic;">debug</span>&#8221; from the end of each line.
  * <span style="font-weight: bold">Note 2:</span> <span style="font-style: italic; font-weight: bold">I have not setup </span><span style="font-weight: bold">/</span><span style="font-weight: bold">etc/pam.d/common-password</span> <span style="font-style: italic; font-weight: bold">so password changing will not affect the domain.</span>
  * <span style="font-weight: bold">Note 3:</span> Using <span style="font-weight: bold">pam_ldap</span> may be a better/easier way to integrate with Active Directory. I haven&#8217;t played with it, but there are [plenty][5] of [resources][6] talking about it.

<small>PS: How do you post code in WordPress without it borking all your newlines and causing much pain and suffering? Please <a href="mailto:michael@susens-schurter.com">let me know</a>.</small>

 [1]: http://www.us.debian.org/
 [2]: http://samba.org
 [3]: http://web.mit.edu/Kerberos/
 [4]: http://www.kernel.org/pub/linux/libs/pam/
 [5]: http://www.oo-services.com/en/articles/sso.html
 [6]: http://adminspotting.net/articles/windows/Linux-and-Active-Directory.html