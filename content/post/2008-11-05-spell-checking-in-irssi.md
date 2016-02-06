---
title: Spell checking in irssi
author: Michael Schurter
layout: post
date: 2008-11-06
url: /2008/11/05/spell-checking-in-irssi/
dsq_thread_id:
  - 463870801
categories:
  - Open Source
  - Technology
tags:
  - irc
  - irssi

---
[irssi][1] is _the client of the future_ and the only real option if you use IRC.

However, one feature I always wished it had was spell-checking. Turns out with about 30 seconds worth of work (including [googling][2]), you can have it!

First on a Debian (probably works on Ubuntu too) system, install Lingua::Ispell and Ispell using the following commands:

<pre lang="bash">$ sudo apt-get install ispell liblingua-ispell-perl
</pre>

It should pull in a number of other packages including a dictionary. I actually received an error as well, but it seems safe to ignore:

`[irssi][1] is _the client of the future_ and the only real option if you use IRC.

However, one feature I always wished it had was spell-checking. Turns out with about 30 seconds worth of work (including [googling][2]), you can have it!

First on a Debian (probably works on Ubuntu too) system, install Lingua::Ispell and Ispell using the following commands:

<pre lang="bash">$ sudo apt-get install ispell liblingua-ispell-perl
</pre>

It should pull in a number of other packages including a dictionary. I actually received an error as well, but it seems safe to ignore:

` 

Next up download the irssi `spell` script:

<pre lang="bash">$ cd ~/.irssi/scripts/
$ wget http://scripts.irssi.org/scripts/spell.pl
$ # Reattach to your irssi screen session now...
$ screen -rAad irssi
</pre>

Finally&#8230;

  1. Load the script into irssi
  2. **bind Alt-s** as the shortcut to spell-check your current line*
  3. tell the script to give you more than the default of 1 guess

&#8230;by running the following commands in irssi:

<pre lang="mirc">/script load spell.pl
/bind meta-s /_spellcheck
/set spell_max_guesses 3
</pre>

And you&#8217;re done! Now when you press Alt-s, irssi spell checks your current line and gives you spelling suggestions in the current window.

<small>* I highlighted this part because the <a href="http://scripts.irssi.org/">irssi scripts page</a> doesn&#8217;t mention it. You have to view <a href="http://scripts.irssi.org/html/spell.pl.html">the documentation at the top of the script file to find out that you have to manually bind the shortcut key</a>.</small>

 [1]: http://irssi.org/
 [2]: http://www.google.com/search?q=irssi+spell+check