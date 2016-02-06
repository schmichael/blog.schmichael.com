---
title: New Cable Internet, 22″ LCD, and WiFi!
author: Michael Schurter
layout: post
date: 2007-12-18
url: /2007/12/17/new-cable-internet-22-lcd-and-wifi/
dsq_thread_id:
  - 577647532
categories:
  - GNU/Linux
  - Open Source
  - Technology
tags:
  - atheros
  - broadband
  - cable
  - comcast
  - debian
  - lcd
  - wifi

---
Today was my work Christmas! I work from home most of the time, so I&#8217;m finally getting around to upgrading some of the equipment I use for my job every day. Today I got 3 new pieces of technology and just finished setting them all up!

**Goodbye ATT&T!**

I switched from 1.5 Mbps/386 Kbps DSL to 10 Mbps/1 Mbps cable broadband today. I used to download packages at 140 KBps to 160 KBps, but now I easily reach over 1 MBps. Tomorrow I get to call AT&T and cancel not only my DSL but also my landline phone.

The only downside is starting in 2008, my local cable company, [Insight][1], is going to become [Comcast][2]. It took me about 10 seconds to get a human on the line when calling Insight. When I tried to call Comcast to find out if anything was going to change, I had to call _3 different phone numbers_ until I finally reached a sales person who kept trying to sell me a package deal for broadband/tv/phone even though Comcast isn&#8217;t in my area yet!

Sales representatives for both companies seemed very confused that a person would only want Internet access. My wife & I watch all of our TV online or through Netflix, and we don&#8217;t need a landline phone. Is that really so strange these days? I suppose most people still have cable TV or satellite, but with more shows becoming available for free online I don&#8217;t see the point.

**Hello 22&#8243; LCD!**

I finally got a nice LCD and got rid of my $5 19&#8243; inch CRT (thanks [Chris][3], it was nice while it lasted). Its a Hanns-G HG216D no frills monitor. There was a similarly priced Acer monitor, by the Hanns-G is Energy Star which I like. It looks beautiful to me, but I have to admit the built-in 1 watt speakers are a complete joke for anything error than error beeps. Luckily they&#8217;re hidden in the back of the LCD case, so no one even has to notice them.

Setup in Linux was as simple as pressing Ctrl-Alt-Backspace in GDM to restart X. It worked as soon as I plugged it in, but restarting X Windows auto-detected the resolution properly so I didn&#8217;t have to mess around in my xorg.conf file.

X Windows has come a very very long way in the past year or two. My xorg.conf file is tiny, and I&#8217;m not sure why I even have it. Last time I tried, X Windows autodetected everything just fine!

Oh come on&#8230; [3 days later and my monitor has already dropped $20 in price. Yeesh.][4]

**Working Wi-Fi in Linux? Yes, but&#8230;**

My office is upstairs, and our only cable connections are downstairs. Instead of running unsightly cables through our house or drilling holes, I just bought a Wi-Fi card for my desktop. Finding a card that works well with Linux was very very difficult.

In the end I bought a [TP-Link TL-WN651G][5] (Ver 1.5), but the box also lists the model as TL-WN650G. Most importantly it works perfectly with the [MadWiFi][6] (it uses an Atheros chipset). Its running at 802.11g with WPA2. The PCI card was only $25, so I didn&#8217;t even have to spend too much more for Linux compatibility. I question the reliability of those $10-$15 adapters anyway&#8230;

The only caveat is caused by Debian&#8217;s insistence on freeness and hatred of binary modules. The MadWiFi module uses a binary module, so Debian makes you download a source package and compile it using `module-assistant`. Now m-a is a wonderful program, but this is still the reason I _always recommend Ubuntu to desktop users._ Expecting anyone other than a Linux hacker to install some random package and run some random command line tool to get WiFi working is deranged.

My motto: Debian is for developers, Ubuntu is for people.

At any rate, I&#8217;ve had a wonderful day and am excited all my new toys play well with Linux.

 [1]: http://www.insight-com.com/
 [2]: http://www.comcast.com/
 [3]: http://blog.christopherpitzer.com/
 [4]: http://www.newegg.com/Product/Product.aspx?Item=N82E16824254024
 [5]: http://www.tigerdirect.com/applications/searchtools/item-Details.asp?EdpNo=3350606&sku=D145-1006
 [6]: http://madwifi.org/