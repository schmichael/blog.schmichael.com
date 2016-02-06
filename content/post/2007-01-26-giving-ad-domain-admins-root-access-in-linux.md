---
title: Giving AD Domain Admins Root Access in Linux
author: Michael Schurter
layout: post
date: 2007-01-26
url: /2007/01/26/giving-ad-domain-admins-root-access-in-linux/
dsq_thread_id:
  - 464027083
categories:
  - GNU/Linux
  - IT
  - Technology

---
The [sudo][1] command makes it very easy to give the [Domain Admins][2], or any Active Directory group, root access on Linux workstations and servers.

The big prerequisite is that you have to have [Samba][3] and Winbind properly setup to authenticate your Linux boxes against Active Directory. Read Samba&#8217;s documentation[[1][4]][[2][5]] and refer to my [InteropWiki][6] notes for help.

Once you&#8217;re able to login into Linux as Active Directory user, running the _id_ command should display something like this:

<p style="font-family: monospace">
  michael@mail:~$ id<br /> uid=13930(michael) gid=10512(domain admins) groups=10512(domain admins),10513(domain users),11006(teachers),11607(sti everyone 2),11608(sti jr. high),11609(sti high school),11610(sti grade school)
</p>

Where _groups=&#8230;_ is a list of the Active Directory groups of which your user is a member.

Run the _visudo_ command as root:

<p style="font-family: monospace">
  michael@mail:~$ su &#8211;<br /> Password: <em>&#8211;root&#8217;s password&#8211;</em><br /> mail:~# visudo
</p>

In the editor (probably _vim_ or _nano_) scroll to the end and add the following line:

<p style="font-family: monospace">
  %domain\ admins ALL= ALL
</p>

The _%_ sign means the following name is a group name, and **you need the backslash in order to use group names with spaces**. Vim&#8217;s syntax highlighting doesn&#8217;t seem to properly parse the group name after you use a slash, but sudo will know what you&#8217;re talking about.

Save the file, exit the editor, and now all of your Domain Admins have root access!

To run a command as root simply prepend the _sudo_ command:

<p style="font-family: monospace">
  michael@mail:~$ sudo aptitude
</p>

You&#8217;ll be asked to enter **_your_ password** (not root&#8217;s!) only once as long as you continue to use _sudo_ within a specific timeout period.

 [1]: http://www.gratisoft.us/sudo/
 [2]: http://technet2.microsoft.com/WindowsServer/en/library/1631acad-ef34-4f77-9c2e-94a62f8846cf1033.mspx?mfr=true
 [3]: http://www.samba.org/
 [4]: http://us3.samba.org/samba/docs/man/Samba-HOWTO-Collection/domain-member.html#ads-member
 [5]: http://us3.samba.org/samba/docs/man/Samba-HOWTO-Collection/winbind.html
 [6]: http://michael.susens-schurter.com/interop/Main_Page