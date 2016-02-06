---
title: 'My Gnome 3.0: A Real Web Desktop'
author: Michael Schurter
layout: post
date: 2009-06-03
url: /2009/06/02/my-gnome-30-a-real-web-desktop/
dsq_thread_id:
  - 476119626
categories:
  - GNU/Linux
  - Open Source
  - Technology
tags:
  - dropbox
  - gnome

---
So I missed the [stream of What I Want for <strike>Christmas</strike> Gnome 3.0][1] by &#8230; a while, but better late than never!*

**The Win**

Essentially what I want for Gnome 3.0 is what [Tomboy just got: a web interface][2] called [Snowy][3]. Part synchronization, part collaboration, all &#8220;cloud&#8221; for those buzzword minded among us.

**The Fail**

Luckily there&#8217;s already Conduit which I think does the synchronization bit&#8230; I say &#8220;I think&#8221; because I&#8217;ve never actually gotten Conduit to work. I drag & drop F-Spot onto the canvas\*\*, neat. I drag & drop Network to the right of F-Spot, neat. Now what? There&#8217;s no configure option for Network. Heck, there&#8217;s not even a Remove\*\** for Network. I right click and select Synchronize in hopes it will prompt me for details, but instead it happily reports synchronization is finished. _Huh?!_

I poke around in Preferences hoping for guidance on how to sync to another computer over a network. Wow. The first tab is fine, but the other 2 tabs are just long lists of text. Wait a second, if you scroll _horizontally_ to the right in the Data Providers tab you can see a checkbox to load/unload them! Why you&#8217;d want this option other than for development, I&#8217;m not sure, but its there if you know where to look.

At this point _Conduit has failed to gain my trust, so I give up._ I&#8217;m fine with Pidgin being crash happy or Eclipse being ridiculously complex to configure. The former isn&#8217;t mission critical and the latter is intended for developers.

However, I&#8217;m expected to entrust all of my files to Conduit. Files and account information for network resources if I could figure out how to get that to work. I have pretty high expectations for anything I&#8217;m entrusting my files and passwords too. Right now Conduit seems more like a demo of GTK+&#8217;s canvas drawing abilities (it is pretty looking) than a powerful synchronization tool.

**The Dream**

_My expectations for web enabling Gnome are **insanely** high._ Synchronization isn&#8217;t enough (although it&#8217;d be an excellent start). I need web enabled collaboration features as well. I need it to Just Work&trade; as well as be Secure By Default&trade;.

This means:

  * All applications can synchronize their _settings_ and _data_.
  * All data has some sort of web viewable format and ideally a way to interact with it on the web as well.
  * By default all settings and data should be _private_.
  * Fine-grained CRUD permissions for all settings and data. The C<small>reate</small> and U<small>pdate</small> are key here: not only should I be able to give other users the ability to edit my files but Grandma should be able to upload photos to my photo album.
  * While I&#8217;m dreaming can I add versioning support ([like Dropbox][4])? Cool, thanks. 😉

**The Implementation**

Unfortunately I think Conduit is the wrong way to go. The concept is sound, but [Worse Is Better&trade;][5]: each application needs to be allowed to implement their own integration with the cloud synchronization and collaboration system. There&#8217;s too many application specific tasks to accomplish intuitive synchronization and collaboration features outside the main application.

Tomboy has had pretty good synchronization for a while now. [Firefox is getting it with Weave][6].

In a way F-Spot and Banshee support 1-way synchronization and collaboration. F-Spot can upload photos to a variety of services which have all (or at least most) of the features I&#8217;m pining for. Banshee&#8217;s ability to download Podcasts and music synchronize to iPods (note: I&#8217;ve never used that feature) is a sort of primordial synchronization. If only [Banshee Web][7] had survived (and wasn&#8217;t written in ASP.NET, the ickiest of all webdev platforms). [Abiword has been toying with cloud services for a little while as well.][8]

Perhaps Evolution is the poster child for this: I currently use it as a Gmail and Gcal interface sometimes because there are certain use cases for which I prefer it (shocking I know!). Despite its past reputation for being bloated and buggy, it Just Works&tm; these days and integrates beautifully with the rest of the Gnome desktop (are those calendar events in my system tray calendar?! amazing! Pidgin integration?! <3 Evolution). Evolution lives completely in the cloud and synchronizes everything locally beautifully (after years and years of effort). **Why Gnome Can Do It**

Gimp is actually the first Gnome app to really make me realize working on the web _can_ and _should_ be as easy as working locally. All it did was utilize Gnome&#8217;s VFS to edit and save images via FTP or SSH. With Gnome&#8217;s screenshot tool, I can save a screenshot to a web accessible location in 1 keypress and 2 clicks. Amazing! Thats almost as fast and easy as using a pastebin tool on the command line for sharing text.

Snowy seems like an excellent poster child for the web interface I&#8217;m whining about. I haven&#8217;t used it yet, but the very idea that Tomboy already has an open source reference implementation is an excellent start. 3rd parties could implement the protocols and offer competing services.

In an ideal world this would create a revenue stream for open source applications: services like Dropbox could support the synchronization and collaboration protocols and in return support development of the projects. The more people who use apps that integrate seamlessly with Dropbox, the more people who pay for Dropbox&#8230; or box.net or Amazon or&#8230; you get the idea.

**FreeDesktop.org Does What?!**

That&#8217;s right, FreeDesktop.org needs to lead the charge here. Its not enough that the protocols are open, application developers need libraries to make synchronization and collaboration _easy_. In that way Conduit is right: each application should not completely reinvent the wheel.

FreeDesktop.org needs to follow Mozilla&#8217;s lead. Mozilla realized early on that in order for their browser business to succeed, they needed _open standards to succeed_. FreeDesktop.org needs to do the same. A KDE application should be able to synchronize to the same service as a Gnome app (this is where Conduit&#8217;s monolithic-master-synchronization-app model seems too optimistic to succeed). OSX and Windows apps should be able to use the base synchronization libraries as well, even if they don&#8217;t use GTK+ or QT.

At the end of the day I should be able to sync my photos, documents, and mp3s between my laptop, desktop, cell phone, Kindle, etc as well as any relevant application settings (Tomboy for Kindle?! yes please!). &#8230;and so much more.

<small>* Not always true. For example: posting opinions on a piece of software long after the roadmap has been made.</small>
  
<small>** Strike 1 against Conduit: &#8220;Canvas&#8221; isn&#8217;t a very end user friendly term <abbr title="in my humble opinion">IMHO</abbr>. A minor complaint, but as confusing as the UI already is, it needs all the help it can get. Perhaps the problem isn&#8217;t the name &#8220;Canvas&#8221; but rather that the fact that it doesn&#8217;t even need to be said. Remove all references to it and just put a textbox that says &#8220;Drop data providers here.&#8221; when the canvas is empty. The &#8220;Clear canvas&#8221; option can just be &#8220;Clear&#8221; as there&#8217;s really only 1 thing that can be cleared.</small>
  
<small>*** Strike 1.5: &#8220;Remove&#8221; would be better than &#8220;Delete&#8221;. Delete makes me wonder if its going to erase my files! Remove seems more descriptive and precise. Also, drop &#8220;item&#8221; from the end of each right click menu option. Its redundant when every option operates on the item you clicked.</small>

 [1]: http://www.google.com/cse?cx=007525575524326405779%3Ac0gv0y410u0&q=gnome+3.0&cof=FORID%3A0
 [2]: http://automorphic.blogspot.com/2009/05/tomboy-0151-release-brings-new-online.html
 [3]: http://live.gnome.org/Snowy
 [4]: https://www.getdropbox.com/referrals/NTE2ODkwNDk
 [5]: http://www.jwz.org/doc/worse-is-better.html
 [6]: https://labs.mozilla.com/projects/weave/
 [7]: http://idea.opensuse.org/content/ideas/web-interface-to-banshee-library
 [8]: http://www.abisource.com/wiki/AbiCollab