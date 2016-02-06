---
title: schmongodb slides from Update Portland
author: Michael Schurter
layout: post
date: 2011-02-03
url: /2011/02/02/schmongodb-slides-from-update-portland/
dsq_thread_id:
  - 463870999
categories:
  - Open Source
  - Technology
tags:
  - mongodb
  - updatepdx
  - urbanairship

---
A few months ago someone in #pdxwebdev on Freenode asked an innocent [MongoDB][1] question. In response I ranted seemingly endlessly about our experience with MongoDB at [Urban Airship][2]. After a few moments somebody (perhaps sarcastically? who can know on IRC) suggested I give a talk on my experiences with MongoDB. That led me to realize despite [Portland&#8217;s amazing meetup culture][3] there were no tech-meetups that focused on either:

  1. Narrative talks based on experiences in production <small>(<em>not</em> how-tos)</small>
  2. Database-agnostic backend systems focused groups <small>(<em>not</em> just a NoSQL meetup)</small>

So I started one: [Update Portland][4].

And I gave my promised MongoDB talk: [schmongodb][5].

And [10gen sent swag][6]! (Thanks to [Meghan][7]! It was a big hit.)

_And_ my brilliant coworker [Erik Onnen][8] gave a short talk on how he&#8217;s beginning to use [Kafka][9] at Urban Airship. (Expect a long form talk on that in the future!)

Thanks to everyone who showed up. I had a great time and have high hopes for the upcoming meetings. (Sign up for the [mailing list][10]!)

The slides may come across as overly negative. After all Urban Airship is actively moving away from MongoDB for our largest and busiest pieces of data. So I want to make 2 things very clear:

  1. I like MongoDB and would like to use it again in the future. There&#8217;s a lot I don&#8217;t like about it, but I can&#8217;t think of any &#8220;perfect&#8221; piece of software.
  2. The IO situation in EC2, particularly EBS&#8217;s poor performance (RAIDing really doesn&#8217;t help) made life with MongoDB miserable. This story may have been very different if we were running MongoDB on bare metal with fast disks.

[Mike Herrick, the VP of Engineering at Urban Airship][11], put me on the spot at the end of my talk by asking me by asking me: **&#8220;Knowing what you know now, what would you have done differently?&#8221;**

I didn&#8217;t have a good answer, and I still don&#8217;t. Despite all of the misadventures, MongoDB wasn&#8217;t the wrong choice. Scaling systems is just hard, and if you want something to work under load, you&#8217;re going to have to learn all of its ins and outs. We initially started moving to Cassandra, and while it has tons of wonderful attributes, we&#8217;re running into plenty of problems with it as well.

So I think the answer is _knowing then what I know now_. In other words: **Do your homework**. That way we could have avoided these shortcomings and perhaps still be happy with MongoDB today. Hopefully these slides will help others in how they plan to use MongoDB so they can use it properly and happily.

**Note:** I added lots of comments to the speaker notes, so you&#8217;ll probably want to view those while looking at the slides.

 [1]: http://www.mongodb.org
 [2]: http://urbanairship.com
 [3]: http://calagator.org/
 [4]: http://www.meetup.com/updatepdx/
 [5]: https://docs.google.com/present/view?id=ddzswzbr_104f2sgp8dq
 [6]: http://twitter.com/meghanpgill/status/23455639216848896
 [7]: http://twitter.com/meghanpgill
 [8]: http://twitter.com/eonnen
 [9]: http://sna-projects.com/kafka/
 [10]: http://groups.google.com/group/update-pdx
 [11]: http://www.mikeherrick.com/