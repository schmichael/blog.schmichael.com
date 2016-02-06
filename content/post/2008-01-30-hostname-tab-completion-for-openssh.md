---
title: Hostname Tab-Completion for OpenSSH
author: Michael Schurter
layout: post
date: 2008-01-30
url: /2008/01/30/hostname-tab-completion-for-openssh/
dsq_thread_id:
  - 463870636
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology
tags:
  - shortcuts
  - ssh

---
I use [OpenSSH][1] daily. In fact the only app I probably use more is [vim][2]. However, until yesterday I was typing out the full username and hostname when using ssh:

`&nbsp;&nbsp;&nbsp;ssh username@ridiculouslylong.domain.com`

**Ugh**

Using the same username makes life a bit simpler:

`&nbsp;&nbsp;&nbsp;ssh ridiculouslylong.domain.com`

**Meh**, better, but I&#8217;m _really_ lazy!

I&#8217;d heard about tab-completion for hostnames from various blogs, but never knew how to do it. I hopped into #debian and thirty seconds later someone had kindly told me about `<b>~/.ssh/config</b>`

Not only is any host listed in your `~/.ssh/config` auto-completed on the command line by hitting tab, but you can also specify what username to connect as! So my .ssh/config file looks something like:

`Host host1.domain.com<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;User randomuser<br />
Host www.somewhereelse.com<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;User someotheruser<br />
Host mail.domain2.com<br />
Host domain3.com`

Now I can just type:
  
`&nbsp;&nbsp;&nbsp;ssh h<TAB><ENTER>`
  
to connect to _host1.domain.com_ as _randomuser_.

**Beautiful.**

Check out `man ssh_config` for details and other options.

Also, if you&#8217;re not using [ssh keys][3] instead of passwords, you&#8217;re doing too much work. [Seahorse][4] makes SSH keys simple.

 [1]: http://openssh.org/
 [2]: http://www.vim.org/
 [3]: http://en.wikipedia.org/wiki/Ssh-agent
 [4]: http://www.gnome.org/projects/seahorse/