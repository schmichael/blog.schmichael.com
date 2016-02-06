---
title: Time to Learn Git?
author: Michael Schurter
layout: post
date: 2009-01-04
url: /2009/01/04/time-to-learn-git/
dsq_thread_id:
  - 463870822
categories:
  - Open Source
  - Python
  - Technology
tags:
  - bzr
  - dvcs
  - git
  - hg
  - version control

---
**Update:** Doh! Sorry for flooding everyone&#8217;s feed readers with my epic post. Evidently WordPress ignored my &#8220;more&#8221; tag. <small>I think I ran into this problem before&#8230;</small>

**Update 2:** Retracted the meaningless Google Trends point. Thanks to commenters for pointing out how meaningless it was. I still feel like git has a much stronger web presence than bzr or hg, but its just another one of the many &#8220;gut feelings&#8221; in this post. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

The DVCS wars have been raging for a while now, and in case you haven&#8217;t been keeping score, **git is winning**. Admittedly I have no proof and don&#8217;t even know if proof is possible, but I have some good evidence of git&#8217;s march toward VCS dominance:
  
<!--more-->

  * [Git dominates every other DVCS by an order of magnitude among Debian packages (that link to their upstream repository).][1]
  * [A recent survey of Gnome developers found an overwhelming support for Git][2] over other VCSes.
  * <del datetime="2009-01-04T18:30:56+00:00"><a href="http://www.google.com/trends?q=git%2Cbzr%2Cmercurial">Git dominates Google trends</a>.</del> <small>Speaking of Google, they have 4 <a href="http://research.google.com/video.html">Tech Talks</a> on Git, and absolutely none for bzr <del datetime="2009-01-05T16:53:00+00:00">or hg</del>. Update: hg has one &#8211; see comments.</small>
  * [Why Git is Better than X][3] &#8211; More than the site, the lack of popular counter-argument sites springing up leads me to believe hg and [bzr][4] don&#8217;t have nearly as fanatical of supporters.

Also note some of the major upstream projects using each DVCS:

<div style="float: left; width: 150px; text-align: left;">
  <strong><a href="http://git.or.cz/gitwiki/GitProjects">git</a></strong></p> 
  
  <ul>
    <li>
      <a href="http://kernel.org/">Linux Kernel</a>
    </li>
    <li>
      <a href="http://git.fedoraproject.org/">Fedora</a>
    </li>
    <li>
      <a href="http://cgit.freedesktop.org/">X.org/FreeDesktop</a>
    </li>
    <li>
      <a href="http://dev.perl.org/perl5/source.html">Perl</a>
    </li>
    <li>
      <a href="http://rubyonrails.org/">Ruby on Rails</a>
    </li>
    <li>
      <a href="http://git.samba.org/">Samba</a>
    </li>
    <li>
      <a href="http://wiki.winehq.org/GitWine">Wine</a>
    </li>
    <li>
      <a href="http://dev.laptop.org/browser">OLPC</a>
    </li>
  </ul>
  
  <p>
    Get the idea yet?
  </p>
</div>

<div style="float: left; width: 150px; text-align: left;">
  <strong><a href="http://bazaar-vcs.org/WhoUsesBzr">bzr</a></strong></p> 
  
  <ul>
    <li>
      <a href="http://dev.mysql.com/tech-resources/articles/getting-started-with-bazaar-for-mysql.html">MySQL</a>
    </li>
    <li>
      <a href="https://wiki.ubuntu.com/Bzr#The%20Bazaar%20or%20%22An%20Explanation%20of%20Bazaar%20for%20the%20(Almost)%20Typical%20Contributor%22">Ubuntu</a>
    </li>
    <li>
      <a href="http://www.list.org/">Mailman</a></a>
    </li>
  </ul>
</div>

<div style="float: left; width: 150px; text-align: left;">
  <strong><a href="http://www.selenic.com/mercurial/wiki/index.cgi/ProjectsUsingMercurial">hg</a></strong></p> 
  
  <ul>
    <li>
      <a href="http://hg.mozilla.org/">Mozilla</a>
    </li>
    <li>
      <a href="http://openjdk.java.net/">OpenJDK</a>
    </li>
    <li>
      <a href="http://xenbits.xensource.com/">Xen</a>
    </li>
    <li>
      <a href="http://pylonshq.com/">Pylons</a><small> (not quite major but it will have to do)</small>
    </li></div> 
    
    <div style="clear:both;">
      &nbsp;
    </div>
    
    <p>
      <strong>Communities</strong>
    </p>
    
    <p>
      Git seems to be attracting the most diverse communities as well:
    </p>
    
    <p>
      <em>Git:</em> Linux Kernel, X.org/FreeDesktop, Ruby on Rails<br /> <em>Bazaar:</em> Ubuntu, Ubuntu, Ubuntu<br /> <em>Mercurial:</em> Pythonistas, projects that need better Windows support than Git offers
    </p>
    
    <p>
      <small>Once again I don&#8217;t really have any stats to back up these assertions, they&#8217;re just my biased observations.</small>
    </p>
    
    <p>
      <strong>Personally&#8230;</strong>
    </p>
    
    <p>
      I tried learning Git soon after it was first released and failed like so many others. Unlike many of those others, I never went back to give it another shot.
    </p>
    
    <p>
      Next I learned Bazaar and felt comfortable in it almost immediately. Now I use Bazaar as my preferred VCS and quite like it mainly because it works well and was very easy to learn. I know its not the fastest, but its so far from being a bottleneck in my development process I don&#8217;t notice.
    </p>
    
    <p>
      I learned Mercurial for work and use it at least as much as Bazaar, but I&#8217;m not sure why anyone would use it over Bazaar. I think people who learned Mercurial first think the same thing about Bazaar. 😉
    </p>
    
    <p>
      And perhaps thats part of why Git is winning. It seems fundamentally different from the other two which is probably why its the only 1 of the 3 I haven&#8217;t learned.
    </p>
    
    <p>
      <strong><em>THE FUTURE!!!!!!!11</em></strong>
    </p>
    
    <p>
      I actually don&#8217;t plan on learning git any time soon. <a href="http://michael.susens-schurter.com/blog/2008/12/27/web-server-quandary/">My time for playing with new technology is currently taken up testing nginx, spawning, and FastCGI</a>.
    </p>
    
    <p>
      I suspect thats the norm as well: people who already know a DVCS <em>probably</em> aren&#8217;t looking to migrate between them. The few that are, are probably moving to Git.
    </p>
    
    <p>
      I think we&#8217;ll see the current trend of Git&#8217;s lead widening over bzr and hg as well.
    </p>
    
    <p>
      However, <em><strong>I don&#8217;t see the war ending anytime soon. The fact of the matter is all 3 of them are great</strong></em> and the weaker DVCSes have already fallen prey to evolutionary forces (monotone, darcs, etc).
    </p>
    
    <p>
      <strong>Flamebait</strong>
    </p>
    
    <p>
      What are your thoughts on my completely contrived DVCS War? Which do you prefer? How many do you use? Are my assumptions about popularity (in particular the various communities around each) accurate?
    </p>
    
    <p>
      <small>I wish <a href="https://www.ohloh.net/">Ohloh</a> or <a href="http://cia.vc/">cia.vc</a> gave VCS usage statistics, although I&#8217;m not even sure they record that data.</small>
    </p>

 [1]: http://upsilon.cc/~zack/stuff/vcs-usage/
 [2]: http://blogs.gnome.org/newren/2009/01/03/gnome-dvcs-survey-results/
 [3]: http://whygitisbetterthanx.com/
 [4]: http://whybzrisbetterthanx.github.com/