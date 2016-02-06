---
title: “a ton of these type of messagizzles”
author: Michael Schurter
layout: post
date: 2005-09-15
url: /2005/09/15/a-ton-of-these-type-of-messagizzles/
dsq_thread_id:
  - 484087318
categories:
  - Open Source

---
The following e-mail just dropped into my inbox via the [clamsmtp-users mailing list][1]: (I italicized the best bits for you)

> Hey dudens!
> 
> I had a problem with this thing that I&#8217;ve fixed myself and now I am going to do the gracious thing and give back to those who have given me so much for so little for a change!
> 
> Given my experience with viruses (I am the fellow who identified with W32.ssl.B virus last year that probably saved people countless billions of dollars in down time) I decided that now would be a good time to get some anti-virus going at the bank that I work for! So I set out to find some free thingy that would do what I need for free so that way I don&#8217;t have to pay somebody for something _and I can get away with it without them noser sons of bizatcheez from the SPA poking their beaks into my business! LLOSLLS!!!_
> 
> So, I was using the ClamSTMP here on a BSD to our Exchange 2000 server. I noticed that about 4 out of 5 emails (or more) were getting lost somewhere in the bit bucket. I put _a clamspmtd into snooper mode and noticed a ton of these type of messagizzles popping onto my box&#8217;s scope:_
> 
> clamsmtpd: 100013: CLIENT: network read operation timed out
> 
> _So what the hecker?!! So I went to the toilet and after a bit of staring at my log_ I thought that these connections that were timing out were always connections that, instead of the DATA command, were using some goofballing proprietary Exchange extension to the SMTP command set! _Score one for Microstof for scooping our their shorts and tossing it our way:_
> 
> clamsmtpd: 100013: CLIENT < XEXCH50 1912 2 clamsmtpd: 100013: SERVER > XEXCH50 1912 2
  
> clamsmtpd: 100013: SERVER < 354 Send binary data clamsmtpd: 100013: CLIENT > 354 Send binary data
> 
> I also saw this after the EHLO command to list capabilities:
> 
> clamsmtpd: 100013: SERVER < 250-XEXCH50 clamsmtpd: 100013: CLIENT > 250-XEXCH50
> 
> So, I modified smtppass.c (I am not a C programmer at all, but I did manage to _make this fat lady sing like the crazy tart she really is just ask the CEO here at the bank because shes good at making them women sing like daisies if you catch my wind_). And here is my diff so you can cut and paste into your own code to solve this glaring, overlooked problem:
> 
> 112a113
  
> > #define ESMTP_XEXCH50 &#8220;XEXCH50&#8221;
  
> 1043a1045
  
> > is\_first\_word(p, ESMTP\_XEXCH50, KL(ESMTP\_XEXCH50)) ||
> 
> This adds XEXCH50 to the list of filtered commands! After doing this, the sending MTA&#8217;s never use XEXCH50 as it is not listed as a capability for your proxied Exchange server and so they will use the standard goodie DATA command instead!
> 
> So you can all thank me now for this patch. I am sure a lot of you folks out there were having this problem and I am glad you are appreciative even if you will never admit it!
> 
> P.S. Check out my bloglog <http://www.bilano.biz/> and you can read about the W32.ssl.b virus! It is very good&#8230;
> 
> &#8212;&#8212;&#8211;
  
> Mr. Billy B. Bilano, MSCE, CCNA
  
> <http://www.bilano.biz/>
  
> Expert Sysadmin Since 2003!
  
> &#8216;C:\WINDOWS, C:\WINDOWS\GO, C:\PC\CRAWL&#8217; &#8212; RMS 

And no, Mr. Billy &#8220;Expert Sysadmin Since 2003&#8221; B. Bilano, I do not catch your wind.

PS &#8211; Nate Nielsen, the developer of [clamsmtp][2], was very professional in his response and it looks like this code will be integrated into the next release.

 [1]: http://sourceforge.net/mail/?group_id=121993
 [2]: http://memberwebs.com/nielsen/software/clamsmtp/