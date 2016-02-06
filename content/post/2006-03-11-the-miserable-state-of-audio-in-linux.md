---
title: The Miserable State of Audio in Linux
author: Michael Schurter
layout: post
date: 2006-03-12
url: /2006/03/11/the-miserable-state-of-audio-in-linux/
dsq_thread_id:
  - 463870047
categories:
  - GNU/Linux

---
So I&#8217;ve been trying to transfer some interviews my Dad did back in the late 1970s with coal miners to my Debian Linux desktop computer for archiving. I have an ancient Sony tape deck hooked into my Line In jack, and once I unmuted Line In in the mixer I could hear the tape playing through my computer&#8217;s speakers.

However, I was completely unable to capture the audio on my computer despite hearing it through my computers speakers and being able to adjust the volume through my mixer.

I went through the 2 million normal steps you have to go through to get audio to work in Linux: run alsaconf, unmute channels, raise volume levels, set capture channel, etc.

Nothing. I tried it with Gnome&#8217;s Sound Recorder utility as well as the command line recorder that comes with ALSA. Gnome&#8217;s Sound Recorder wouldn&#8217;t do a thing. ALSA&#8217;s sound recorder at least captured static.

So then I thought perhaps I&#8217;ll try one of the millions of more powerful audio utilities for Linux. I began to venture into the world of JACK, Audacity, and other applications with horrible UIs and cryptic options. The various JACK tools I played with gave me a dazzling array of channels that I think I could hook up to one another and monitor and adjust and record and &#8230; nothing ever happened.

So as far as I can tell audio in Linux is the most confusing jumble of technologies and acronyms and is a pretty good example of what happens when open source hackers refuse to standardize.

Just for kicks here are the various audio technologies/tools I played with: [OSS Compatibiltiy in ALSA][1], [ALSA][2], [JACK][3], [JACKEQ][4], [LADSPA][5], ESD (likes to crash), [GStreamer][6], Gnome Sound Recorder, [Audacity][7], and a couple other utilities.

 [1]: ftp://ftp.alsa-project.org/pub/oss-lib/
 [2]: http://www.alsa-project.org/
 [3]: http://jackit.sourceforge.net/
 [4]: http://jackeq.sourceforge.net/
 [5]: http://www.ladspa.org/
 [6]: http://gstreamer.freedesktop.org/
 [7]: http://audacity.sourceforge.net/