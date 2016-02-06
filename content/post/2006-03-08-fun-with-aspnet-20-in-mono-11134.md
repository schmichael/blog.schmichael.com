---
title: “Fun” with ASP.Net 2.0 in Mono 1.1.13.4
author: Michael Schurter
layout: post
date: 2006-03-08
url: /2006/03/08/fun-with-aspnet-20-in-mono-11134/
dsq_thread_id:
  - 463870020
categories:
  - GNU/Linux
  - Mono/.Net
  - Open Source

---
I tried to get the ASP.Net 2.0 project we&#8217;re working on at [Synthesys][1] running on [Mono][2]. The server runs [Debian Linux][3] [Etch][4], and I use the following packages (some of them are [preview packages][5]):

  * mono (and related libraries) 1.1.13.4-0pre6
  * mono-xsp2 (and mono-xsp2-base) 1.1.13-1

xsp2 works beautifully, and seems to print out nice debugging information either in the browser on or the server when exceptions are thrown. Unfortunately exceptions are thrown a lot. Here are some of the differences between Microsoft&#8217;s and Mono&#8217;s ASP.Net 2.0 implementations that I ran into:

  1. Mono does not support `Culture="Auto"` (or &#8220;auto&#8221;). Switching to `Culture="en-US"` works, but isn&#8217;t desirable.
  2. CodeFile paths must be absolute from the root of your project. We had a MasterPages folder with a file that specified a CodeFile in the same folder with `CodeFile="nameOfCodeFile.cs"`, but Mono wanted it to be `CodeFile="MasterPages/nameOfCodeFile.cs"`.
  3. Mono seemed to want only integers for measurements in ASP.Net tag attributes that only accept pixel measurements. So &#8220;10px&#8221; needed to be just &#8220;10&#8221;. I&#8217;m not sure precisely which attributes this applies to as I just changed them all. (I know it does not apply to font sizes.)
  4. Mono 1.1.13 does not contain a definition for `Page.Title`, only `Page.Header.Title`. This appears to be fixed in the trunk.
  5. Page.Theme and Page.StyleSheetTheme aren&#8217;t supported in 1.1.13, but my new hero, [Chris Toshok][6], [just added them][7].
  6. So far not to bad, but now for the show stopper: my custom **SiteMap** implementation. A quick glance at [Mono&#8217;s Class Status][8] page shows SiteMap related classes to be almost done, but I still get the following exception: 
    <pre>System.NullReferenceException: Object reference not set to an instance of an object
in &lt;0x0008d> System.Web.SiteMap:Init ()
in &lt;0x00007> System.Web.SiteMap:get_Provider ()
in &lt;0x0000a> System.Web.SiteMap:get_CurrentNode ()
in &lt;0x0000d> MasterPages_default:Page_Load (System.Object sender, System.EventArgs e)
in (wrapper delegate-invoke) System.MulticastDelegate:invoke_void_object_EventArgs (object,System.EventArgs)
in &lt;0x00117> System.Web.UI.Control:OnLoad (System.EventArgs e)
in &lt;0x00112> System.Web.UI.Control:LoadRecursive ()
in &lt;0x00161> System.Web.UI.Control:LoadRecursive ()
in &lt;0x001c4> System.Web.UI.Page:InternalProcessRequest ()
in &lt;0x000a7> System.Web.UI.Page:ProcessRequest (System.Web.HttpContext context)</pre>

I have high hopes that the next release of Mono will improve ASP.Net 2.0 support considerably. Hopefully I can start helping submit bug reports and testing new features as well!

 [1]: http://www.synthesyssolutions.com
 [2]: http://mono-project.com/ASP.NET#ASP.NET_2.0
 [3]: http://www.debian.org
 [4]: http://www.us.debian.org/releases/etch/
 [5]: http://debian.meebey.net/
 [6]: http://squeedlyspooch.com/blog/
 [7]: http://squeedlyspooch.com/blog/archives/002033.html
 [8]: http://mono.ximian.com/class-status/mono-HEAD-vs-fx-2/class-status-System.Web.html