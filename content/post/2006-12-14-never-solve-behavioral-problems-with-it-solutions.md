---
title: Never Solve Behavioral Problems with IT Solutions
author: Michael Schurter
layout: post
date: 2006-12-14
url: /2006/12/14/never-solve-behavioral-problems-with-it-solutions/
dsq_thread_id:
  - 600880915
categories:
  - IT

---
I learned a valuable lesson from my boss yesterday: never try to solve behavioral problems with purely IT solutions. IT solutions should reflect and possibly augment social/organizational rules, not create them.

**Case 1:** a teacher wanted to lock down a computer so only certain students could login to it. Since we use Active Directory I proposed using GPOs to enforce local login restrictions on the computer. My boss knew better. He asked the teacher _why_ she wanted these restrictions and it turns out it was just students arguing about who got to use the computer.
  
Her plan was to just lock out half of the students which doesn&#8217;t really solve the underlying social problem of the students being unable to share resources. In fact it only increases bitterness and encourages the locked out students to find loopholes.

**Solution:** The teacher should use her authority to facilitate student cooperation.
  
**Case 2:** at a small organization (approximately 100 workstations) I consulted at before I began working at the Tremont School District we were running out of bandwidth on our Internet connection. The company had come to rely on the Internet for many business-critical services, so I was tasked with ensuring there was plenty of bandwidth available (without spending money of course).
  
It didn&#8217;t take long to figure out that a significant number of employees had Internet radio playing all day. Not a big problem until someone also forwards around a link to a funny Internet video and suddenly everyones fighting for bandwidth.

**My solution:** Ask users&#8217; not to listen to Internet radio for the time being and respect that the Internet is part of the company&#8217;s critical infrastructure (not a toy!). Then add a DSL line to handle user web traffic while the T1 is used for business-critical functions.

**Administrations solution:** Block Internet radio and only inform users when they complain.

So I got tasked with setting up a myriad of seemingly random firewall rules in an attempt to block Internet radio. Of course a lot of Internet media is delivered via plain old HTTP, so I had to start blocking popular radio sites as well.
  
This mostly solved the bandwidth issues but caused a lot of user frustration and is very difficult to maintain. This solution also encouraged users to simply find loopholes because we never actively sought a **behavioral** change.

The moral of the story is that IT workers should always attempt social/behavioral solutions to IT-related issues alongside IT solutions. Its like if your mother keeps calling early on Saturday mornings. You could unplug the phone, but maybe you should mention to her that you don&#8217;t get up at 8am on the weekends first. <img src="http://localhost/wp-includes/images/smilies/simple-smile.png" alt=":)" class="wp-smiley" style="height: 1em; max-height: 1em;" />