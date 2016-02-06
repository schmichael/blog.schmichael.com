---
title: Revoking My Fan Boy Status
author: Michael Schurter
layout: post
date: 2007-02-21
url: /2007/02/21/revoking-my-fan-boy-status/
dsq_thread_id:
  - 900876607
categories:
  - GNU/Linux
  - Open Source
  - Technology

---
Its been brought to my attention that since I&#8217;ve started using Linux as my primary operating system at work, I&#8217;ve become a bit overzealous. I appear to have fallen in with [the wrong crowd][1]. 😉
  
So here&#8217;s a list of my <span style="font-weight: bold">gripes with Linux</span> and another list of <span style="font-weight: bold">what I like about Windows</span>. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

**Linux Gripes**

  * **Flaky Sound** &#8211; My sound support in different applications was pretty hit or miss until one day I discovered you need to install **libesd-alsa0** to use Gnome+ESD+ALSA instead of **libesd** which seemed to break all non-ESD enabled apps (like games and Iceweasel/Firefox) because libesd locks /dev/dsp which non-ESD enabled apps like to lock as well.
  * **Debian Zealotry** &#8211; I like Debian, but they&#8217;re so focused on freedom that users are sometimes forgotten. Take _Iceweasel vs. Firefox_ for example. I don&#8217;t agree 100% with Mozilla Corp., but **renaming the most recognizable application in the entire system is unacceptable**. Not only that but Debian just recently decided to switch profile directories, so I had to go scrabbling through hidden folders to recover my old bookmarks and settings. Besides Firefox there&#8217;s also the whole proprietary driver issue. While **hate proprietary drivers they are an unfortunate fact of life** for now. Whether its video or wi-fi drivers, users just need their devices to work.
  * **[RTFM][2]** &#8211; Most every open source project I use has great documentation&#8230; **somewhere**. The problem is I never know where. Is it in the **man** page? Is it in the **/usr/share/doc/_package-name_/** folder? Is it on a **web site**? Or is it actually built into the application?
  
    The documentation could be in any one of those places or perhaps multiple. Or better yet: there are different versions or formats in each location&#8230; ugh&#8230;
  * <span style="font-weight: bold">There&#8217;s no standard for installing 3rd party binaries.</span> Don&#8217;t misunderstand me &#8211; I love package based systems and package managers. Having to browse the web, download, and install 3rd party apps on Windows feels clumsy now. However, there are times when I&#8217;d like to install an application that doesn&#8217;t have a Debian package, and I don&#8217;t really want to compile it from source. There&#8217;s <span style="font-weight: bold">no good solution for this.</span>

<span style="font-weight: bold">What I Like About Windows</span>

  * Windows XP is a stable operating system with excellent device support. If Windows 2000 was still supported by Microsoft, I would feel the same way about it.
  * Nearly everything in Windows can be configured via a GUI application. Its much easier to configure things in Windows by just poking around Control Panel.
  * Tons of documentation. Between Technet, the KnowledgeBase, and MSDN, Microsoft provides mountains of documentation for their huge range of products. It can be hard to search and navigate, but there&#8217;s a ton of information to sort through.
  * Sensible folder names. I appreciate <span style="font-style: italic">/usr/bin</span> over <span style="font-style: italic">C:\Program Files\</span> when typing, but trying to explain what <span style="font-style: italic">/etc</span> means to new users is so awkward its embarrassing.

 [1]: http://slashdot.org
 [2]: http://en.wikipedia.org/wiki/RTFM