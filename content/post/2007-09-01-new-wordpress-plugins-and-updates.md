---
title: New WordPress Plugins and Updates
author: Michael Schurter
layout: post
date: 2007-09-02
url: /2007/09/01/new-wordpress-plugins-and-updates/
dsq_thread_id:
  - 463870542
categories:
  - Open Source
  - PHP
  - Python
  - Technology
tags:
  - navel gazing

---
<div style="margin: 6px; float: right">
  <a href="http://wordpress.org" title="WordPress"><img src="http://michael.susens-schurter.com/blog/wp-content/uploads/2007/09/wordpress-screenshot.png" alt="WordPress Screenshot" /></a>
</div>

I just added the **[Subscribe to Comments][1]** WordPress plugin. You should now be able to get e-mail notifications when new comments are posted. This should make flamewars and trolling much easier. 😉

For what its worth I also installed the **[Google Sitemap Generator][2]** plugin which seems to work alright. My main gripe is that the author uses a blog post dated June 5, 2005 as the home page for the plugin! I actually passed it up and kept looking the first time I hit the page because I assumed the plugin was old.

I have to admit, sites that use a blog like a full-fledged CMS usually annoy me. Of course tons of sites probably do it without me noticing, so I suppose if its done well, I don&#8217;t mind. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

A while ago I installed the **[WP-Syntax][3]** plugin. Here&#8217;s a snippet of Python to test it out since I haven&#8217;t gotten around to posting any code lately:

<pre lang="python">d = {'test1': 'hello world'}
d.setdefault('test1', 'goodbye world')
d.setdefault('foo', 'bar')
print d['test1']
print d['foo']</pre>

This prints:

<pre>hello world
bar</pre>

becase setdefault() only changes the value of a dictionary key if the key has no value. Very handy.

My final bit of WordPress hacking has been to switch to using [**Subversion**][4] to update WordPress. Juggling files to do updates is just annoying. With Subversion I just checked out `http://svn.automattic.com/wordpress/branches/2.2` and run `svn up` whenever an update is released.

I suppose I could just schedule running `svn up` with a cron job. It would even automatically e-mail what files it updates because cron e-mails stdout by default. But considering how much I _love_ automatic updates on Windows, I think I&#8217;ll hold off on that&#8230; 😉

**Update:** Grrr&#8230; Now if only I could convince WordPress not to convert my <div> tags to <p> tags when editing posts and messing up my whitespace when saving!

 [1]: http://txfx.net/code/wordpress/subscribe-to-comments/
 [2]: http://www.arnebrachhold.de/2005/06/05/google-sitemaps-generator-v2-final
 [3]: http://wordpress.org/extend/plugins/wp-syntax/
 [4]: http://subversion.tigris.org/