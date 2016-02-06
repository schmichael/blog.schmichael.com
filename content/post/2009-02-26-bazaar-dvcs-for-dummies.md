---
title: 'Bazaar: DVCS for Dummies'
author: Michael Schurter
layout: post
date: 2009-02-26
url: /2009/02/26/bazaar-dvcs-for-dummies/
dsq_thread_id:
  - 464142552
categories:
  - Open Source
  - Technology
tags:
  - bzr
  - dvcs
  - git
  - hg
  - ssh
  - svn

---
I like [Bazaar (bzr)][1]. It doesn&#8217;t make me popular in the [Mercurial][2]-centric Pythonosphere. It doesn&#8217;t make me a 1337 Ã¼ber hacker like [git][3] would.

However, it does meet the most important criteria: **It just works** _for me_.

Now for the big disclaimer: Most of the projects I use bzr to manage fall into 1 of 2 categories:

  1. Projects with small teams (1-4 developers)
  2. Public projects where I just want to grab the source and maybe maintain some local patches

If I needed to somehow manage a project with dozens or hundreds of contributors (like Gnome or the Linux Kernel), git would probably look a lot more appealing to me. After all, it was designed for large code bases with lots of contributors and branches.

I&#8217;ve seen lots of [git cookbooks popping up lately][4], so I thought I&#8217;d explain my bzr workflow for the 2 use cases I list above.

**1. Starting and sharing a project with a small team**
  
Prerequisite: You&#8217;ve created a directory with some code in it.

  1. Turn your source code directory into a bzr repository: <pre lang="bash">~/src/foo$ bzr init</pre>

  2. Add you source files: <pre lang="bash">~/src/foo$ bzr add</pre>

  3. Commit: <pre lang="bash">~/src/foo$ bzr ci</pre>

  4. Push my changes to a remote location* other team members can access: <pre lang="bash">~/src/foo$ bzr push --remember sftp://some/file/server</pre>

Done! My favorite part is that besides the `--remember` option, bzr just does what you expect without any flags or configuring. The `--remember` option simply tells bzr to use that location for future `push` commands (so you can drop all the typing after &#8220;push&#8221;).

For more information check out the [excellent bazaar documentation on sharing code][5].

**2. Getting the code for an open source project**

Unfortunately most big bzr-hosted projects are on Launchpad which makes for a pretty boring demonstration:

<pre lang="bash">~/src$ bzr branch lp:terminator # yawn
</pre>

To make matters worse, non-Launchpad hosted projects are nearly as dull:

<pre lang="bash">~/src$ bzr branch http://bzr.savannah.gnu.org/r/gnash/trunk
</pre>

In each case bzr will create a new directory for you using the last part of the source path (terminator & trunk respectively). You can optionally give it a second argument to put the branch in a different location. The destination can even be a remote server!

<pre lang="bash">~/src$ bzr branch http://source/branch sftp://destination/branch
</pre>

Ok now I&#8217;m just showing off. I&#8217;ve never found a use for that feature. 😉 However, I do appreciate that a location is a location to bzr regardless of whether that location is the local filesystem or a remote server. It just works how you&#8217;d expect it.

[Chapters 4-6 of Bazaar&#8217;s documentation][6] give some excellent examples of various collaboration workflows.

**_Bonus Feature:_ Subversion mode!**

So its not really _Subversion mode_, but bzr does support pulling repositories via the `checkout` command and updating your working copy from the remote repository via the `update` command just like Subversion. As you would expect, the `commit` now sends changes directly to the remote server.

While I&#8217;ve used this feature mainly to make transitioning to bzr easier for Subversion users, [Bazaar&#8217;s documentation has some excellent techniques for making advanced workflows easier using checkouts][7].

* * ** SSH Tips: </p> 

  * bzr+ssh is faster than plain old sftp but requires bzr to be installed on the server.
  * Setup ssh connection multiplexing using `ControlMaster` in `~/.ssh/config` and leave an ssh session active to speed up bzr operations.

 [1]: http://bazaar-vcs.org/
 [2]: http://www.selenic.com/mercurial/
 [3]: http://whygitisbetterthanx.com/
 [4]: http://www.nardol.org/2009/2/19/git-basics-reversing-the-git-sucks-effect
 [5]: http://doc.bazaar-vcs.org/bzr.dev/en/user-guide/index.html#sharing-with-peers
 [6]: http://doc.bazaar-vcs.org/bzr.dev/en/user-guide/index.html
 [7]: http://doc.bazaar-vcs.org/bzr.dev/en/user-guide/index.html#using-checkouts