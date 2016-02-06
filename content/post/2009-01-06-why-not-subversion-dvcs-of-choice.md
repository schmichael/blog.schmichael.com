---
title: Why not Subversion + DVCS of Choice?
author: Michael Schurter
layout: post
date: 2009-01-07
url: /2009/01/06/why-not-subversion-dvcs-of-choice/
dsq_thread_id:
  - 472091872
categories:
  - Open Source
  - Technology
tags:
  - bzr
  - dvcs
  - gnome
  - hg
  - svn
  - version control

---
[A follow-up to my last post on DVCSes&#8230;][1]

[Gnomers][2] have been [discussing DVCSes a lot lately][3], and at least one seems to prefer [bzr as the repository format and git as the protocol it speaks.][4] <small>If this sounds like madness to you, you&#8217;re not alone.</small>

_What I don&#8217;t understand is why more people don&#8217;t choose to keep Subversion as their repository and just use the $DVCS-svn of your choice?_

Granted I&#8217;ve only used [bzr-svn][5] a bit, but it worked quite well and seems to only be getting better. I hear [git-svn][6] is quite good as well (but <abbrev title="if I remember correctly">iirc</abbrev> hg lags behind the competition).

The benefits of this seem pretty nice:

  * Repository and Project management tools could get by with only first class Subversion support.
  * Directing inexperienced users to download code would be standardized.
  * Linux distributions wouldn&#8217;t have to ship 5 different VCSes (cvs, svn, git, bzr, hg), although the VCSes don&#8217;t take up much space.
  * Developers could use whichever tool they preferred, publish branches to any one of the zillions of free hosts for their DVCS of choice, and get on with their life.

**Answering my own question&#8230;**

The obvious counter argument is that in order to share code you either:

  * &#8230;force everyone who cares to use your DVCS.
  * &#8230;or lose some of the benefits of your chosen DVCS and share code via a SVN branch.

Lets face it, both options are a pretty big hassle for _developers_. Comprises always are.

For smaller single projects the overhead associated with going this route probably isn&#8217;t worth it. You&#8217;ll probably either end up losing 75% of what makes a DVCS handy or just use SVN.

**Why is Gnome not considering this option though?**

This option seems ideal for projects like Gnome. Individual modules will probably adopt a preferred DVCS, and thats fine. None of them are so different that a competent developer couldn&#8217;t yank some revisions from an unfamiliar DVCS.

The project as a whole (and individual modules) would continue to remain uniformly easily available through a single svn checkout.

At the very least isn&#8217;t this better (at least saner) than bolting git onto bzr&#8217;s repository format?

**Audience Participation**

I&#8217;m not a Gnome developer though. Just a curious user. However, as a fellow developer I am left wondering: why isn&#8217;t this a good option? Are $DVCS-svn connectors just not good enough? Are the comprises too great? Or the most likely: am I just missing some obvious showstopper?

 [1]: http://michael.susens-schurter.com/blog/2009/01/04/time-to-learn-git/
 [2]: http://planet.gnome.org/
 [3]: http://wingolog.org/archives/2009/01/06/git-and-bzr
 [4]: http://blogs.gnome.org/johncarr/2008/12/11/dvcs-for-gnome/
 [5]: http://bazaar-vcs.org/BzrForeignBranches/Subversion
 [6]: http://www.kernel.org/pub/software/scm/git/docs/git-svn.html