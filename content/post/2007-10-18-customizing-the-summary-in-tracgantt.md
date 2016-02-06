---
title: Customizing the Summary in TracGantt
author: Michael Schurter
layout: post
date: 2007-10-19
url: /2007/10/18/customizing-the-summary-in-tracgantt/
dsq_thread_id:
  - 463870587
categories:
  - Open Source
  - Python
  - Technology
tags:
  - Lo-Fi Art

---
<div style="float: left; margin-right: 10px;">
  <a href="http://trac.edgewall.org"><img src="http://michael.susens-schurter.com/files/trac_logo.png" alt="Trac Logo" /></a>
</div>

We use [Trac][1] at Lo-Fi Art to manage&#8230; well just about everything that doesn&#8217;t go in our Google Calendars. We&#8217;ve been testing out [TracGantt][2] to get some sort of idea what we&#8217;re working on at any given date.

We quickly ran into the problem that the summary TracGantt displayed didn&#8217;t display 2 pieces of information that were critical for us: the reporter and component. Luckily it wasn&#8217;t very hard to hack in a customizable summary display.

You can download either a&#8230;

  * &#8230;[patch against TracGantt 0.3.2a][3]
  * &#8230;or [an egg][4] which can be placed in your `plugins` folder

To change th summary display simply set: 

<pre lang="ini">summary_format = $foo: $bar</pre>

where $foo and $bar are any keys inside the ticket.values dict. It defaults to: 

<pre lang="ini">summary_format = [$component] $reporter: $summary</pre>

It appears [Will Barton, the creator of TracGnatt, isn&#8217;t very interested in maintaining it][5].

Does anybody else use TracGnatt? Should I offer to become the new maintainer?

 [1]: http://trac.edgewall.org
 [2]: http://willbarton.com/code/tracgantt/
 [3]: http://michael.susens-schurter.com/code/TracGantt-0.3.2a-summary_template.patch
 [4]: http://michael.susens-schurter.com/code/TracGantt-0.3.2a.schmichael-py2.4.egg
 [5]: http://willbarton.com/