---
title: Specs … what are they good for?
author: Michael Schurter
layout: post
date: 2005-10-02
url: /2005/10/02/specs-what-are-they-good-for/
dsq_thread_id:
  - 684355330
tags:
  - Synthesys

---
Quite a coincidence that [Linus Torvalds posts a rant about specs][1] right after I posted about a 49 (now well over 50) page spec I just wrote. While Linus was referring more to hardware specs in relation to operating system kernel programming, I think it definitely applies to specifications in general.

When I began writing the requirments specification I completely felt Linus&#8217;s sentiment of &#8220;[a] spec is close to useless.&#8221; However, at first I didn&#8217;t realize the finer point that Linus went on to make:

> Specs are a basis for _talking about things_. But they are _not_ a basis for implementing software. 

While the client does expect software to be implemented based on these specifications, the process through which that occurs is far less direct than they realize. The spec is just so everyone can talk about the site using the same terms and having the same end goals.

Implementations of the specification will vary so widely as to lead the technically minded into believing the specification had no purpose. However, without the specification, the client and vendor would have no common language with which to speak about the project.

 [1]: http://kerneltrap.org/node/5725