---
title: Wireless Bridges are a Scam
author: Michael Schurter
layout: post
date: 2007-12-18
url: /2007/12/18/wireless-bridges-are-a-scam/
dsq_thread_id:
  - 471399458
categories:
  - GNU/Linux
  - IT
  - Open Source
  - Technology
tags:
  - access point
  - bridge
  - linksys
  - tomato
  - wifi

---
Disclaimer: I am not a hardware guy. The days when I enjoyed cracking open a computer case and poking around are long since past. These days if I can&#8217;t fix something via keyboard, I want no part of it.

Unfortunately, for a client I needed to extend a LAN from Building A across 30 feet of asphalt to Building B. Time to don my Net Admin hat to install a nice straightforward WiFi bridge.

Despite already owning a [Linksys WRT54G series router][1], I decided to just pickup 2 Linksys [WET54G][2] wireless bridges (version 3.1). The **bridges are actually _more_ expensive than routers.** But that just means they&#8217;re better suited for their simple task, right? Wrong&#8230;

The 2 WET54Gs have been nothing but trouble for me. Their web interface sometimes redirects to the hardcoded IP address. They drop their connection and require resetting a lot. They just don&#8217;t work reliably.

So I flashed the WRT54G with Tomato firmware to replace one of the WET54Gs, and so far things are working much better.

If I&#8217;ve never mentioned it before: **I love [Tomato][3] firmware.** I&#8217;ve been using it at home for ages and **never** have to reset it. The [features][4] are outstanding (QoS with ACK Prioritization is a lifesaver when working over SSH).

From now on anytime I need a WiFi router, access point, or bridge, I&#8217;m going to buy a WRT54G and put Tomato on it. Its cheaper than buying specialized Access Points or Bridges and has lots more features.

Did I mention Tomato generates sexy real-time graphs in SVG? Have a screenshot:

<div>
  <a href="http://michael.susens-schurter.com/files/tomato-firmware.png"><img src="http://michael.susens-schurter.com/files/tomato-firmware.thumb.png" alt="Tomato Firmware Bandwidth Graph" /></a>
</div>

 [1]: http://en.wikipedia.org/wiki/WRT54G
 [2]: http://www.linksys.com/servlet/Satellite?c=L_Product_C2&childpagename=US%2FLayout&cid=1134692497433&pagename=Linksys%2FCommon%2FVisitorWrapper&lid=9743339789B32
 [3]: http://www.polarcloud.com/tomato
 [4]: http://en.wikibooks.org/wiki/Tomato_Firmware#Features