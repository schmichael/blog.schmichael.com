---
title: 'Gnome Feature Idea: View Output'
author: Michael Schurter
layout: post
date: 2007-08-02
url: /2007/08/02/gnome-feature-idea-view-output/
dsq_thread_id:
  - 785294487
categories:
  - GNU/Linux
  - Technology

---
From time to time applications crash (I&#8217;m looking at you [Pidgin][1]*). To diagnose the crash I usually start the application in a terminal to watch what it outputs. Most Linux applications noisily dump all kinds of information to the terminal (more accurately, to [stdout and stderr][2]). Usually I can find the source of the crash and sometimes its even something I can fix (in Firefox&#8217;s case it used to mean uninstalling Flash, although thats been quite stable lately too).

What would be nice is if I could easily view the stdout/stderr output of any application. I created a mockup in Gimp of where this feature would be handy:

[![View Output Mockup][3]][4]

For example if [Rhythmbox][5] has been crashing or behaving strangely, you could select View Output and watch its output in a new terminal window. Ideally a small specialized application would handle the output and add useful data like the return status when the process exits.

I&#8217;m guessing [Metacity][6] would be the ideal implementation point so that all graphical applications could automatically benefit.

Honestly, I&#8217;m not sure if a process can redirect or capture another running processes stdout/stderr, so perhaps a session daemon could capture all X applications&#8217; output, send it to ~/.xsession-errors by default, and provide a D-Bus or similar interface to allow for redirection of arbitrary PIDs.

Just a random thought. No clue if it&#8217;d be useful to anyone else, but the current method of either sorting through ~/.xsession-errors or starting the application from the terminal seems suboptimal and inappropriate for most end users.

Now to just convince someone else to implement it&#8230; <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

<small>* Don&#8217;t think you&#8217;re innocent Evolution and Firefox. Although the latest versions of each of these applications have been extremely stable. In the past they&#8217;ve each caused a fair amount of frustration.</small>

 [1]: http://pidgin.im
 [2]: http://en.wikipedia.org/wiki/Standard_streams
 [3]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/08/view-output-mockup.thumbnail.png
 [4]: http://michael.susens-schurter.com/blog/wp-content/uploads/2007/08/view-output-mockup.png "View Output Mockup"
 [5]: http://www.gnome.org/projects/rhythmbox/
 [6]: http://en.wikipedia.org/wiki/Metacity