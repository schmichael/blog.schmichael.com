---
title: More ASP.Net 2.0 features missing from Mono 1.1.13.4
author: Michael Schurter
layout: post
date: 2006-03-08
url: /2006/03/08/few-other-aspnet-20-features-missing-from-mono-11134/
dsq_thread_id:
  - 463870021
categories:
  - Mono/.Net
  - Open Source

---
After stripping out the SiteMap Provider, Membership Provider, and Role Provider, I discovered a few more ASP.Net 2.0 features that are missing from Mono 1.1.13.4:

  1. `System.Web.UI.WebControls.BulletedList:Render` is not implemented. That seems like an easy place for me to learn Mono hacking! We&#8217;ll see what happens&#8230;
  2. `meta:resourcekey` attributes aren&#8217;t recognized which seems strange to me since usually open source projects have excellent I18N and L10N support.
  3. And another showstopper: Mono/XSP2 doesn&#8217;t seem to support automatically loading/compiling files from `App_Code`. I kind of suspected this was some magic on Visual Studio&#8217;s part, but hopefully its something Mono can still implement.