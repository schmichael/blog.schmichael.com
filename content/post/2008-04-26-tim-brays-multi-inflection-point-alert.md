---
title: Tim Bray’s Multi-Inflection-Point Alert
author: Michael Schurter
layout: post
date: 2008-04-26
url: /2008/04/26/tim-brays-multi-inflection-point-alert/
dsq_thread_id:
  - 470917156
categories:
  - Technology

---
While lots of people wiser than I have already commented on [Tim Bray&#8217;s excellent Multi-Inflection-Point Alert post][1], I&#8217;m eager to avoid housework today. 😉

> &#8230;weâ€™re simultaneously at inflection points in programming languages and databases and network programming and processor architectures and Web development and IT business models and desktop environments. Did I miss anything?

Ugh, I feel like I&#8217;m drowning in all of these areas. I&#8217;ve basically given up on keeping up with networking administration and technology (just give me HTTP and I&#8217;m happy).

I&#8217;m happy with my vanilla Gnome desktop environment, but I still have to be proficient with Microsoft Windows in order to survive. I&#8217;d love to be proficient with OSX, but I don&#8217;t have the money for Apple hardware (or the desire to learn yet-another-desktop-environment for that matter).

This is why documentation is so important and should often assume nothing about its reader&#8217;s knowledge. I&#8217;m sure there of lots of people jumping directly into TurboGears and Django development without knowing the basics of Python development like the interactive console and easy_setup.

> CORBA is dead. DCOM is dead. WS-* is coughing its way down the slope to dusty death. REST, they say, is the way to go.

Thank God! As a web developer I find myself preaching the gospel of REST+HTTP+JSON over XML based technologies like SOAP and XMLRPC. [Tim Bray actually had a great post about JSON vs. XML][2] a couple of years ago to which I&#8217;d only add: &#8220;Use XML only if you absolutely have to.&#8221; 😉

> &#8230;I think that SQLâ€™s brain-lock on the development community for the past couple of decades has been actively harmful, and Iâ€™m glad that itâ€™s now OK to look at alternatives.

I&#8217;ve been doing a very poor job of evangelizing this very point to a couple of my friends who develop primarily on PHP and MySQL. SQL is really really great for certain use cases, but forcing yourself to always have to think of object persistence in terms of SQL tables is just masochistic.

> &#8230;itâ€™s increasingly starting to look like threading is a bad idea; donâ€™t go there.

As a pro-GIL Python developer, I obviously couldn&#8217;t agree more! The venerable [Donald Knuth recently chastised hardware manufacturers as well for pushing software developers toward ubiquitous parallelism][3].

That being said, I think threads definitely have good uses. I just disagree with some people&#8217;s [Code Parallel or Die][4] mentality.

I think someone at PyCon this year basically summed up my feelings on threading for _server_ applications: &#8220;If it needs to scale to multiple cores, it probably needs to scale to multiple machines which threading doesn&#8217;t help with at all.&#8221;

(I haven&#8217;t written a non-trivial desktop app in years, so perhaps threading is more useful there.)

> Now all of a sudden itâ€™s PHP and then Rails and a bunch of other frameworks&#8230;

No mention of Python&#8230; ouch. I think once [Django][5] hits 1.0 that will change though.

Go read the **Business Models** and **Desktops** sections for yourself. They&#8217;re fantastic. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

 [1]: http://www.tbray.org/ongoing/When/200x/2008/04/24/Inflection
 [2]: http://www.tbray.org/ongoing/When/200x/2006/12/21/JSON
 [3]: http://www.informit.com/articles/article.aspx?p=1193856
 [4]: http://port25.technet.com/archive/2008/04/14/code-parallel-or-die.aspx
 [5]: http://www.djangoproject.com/