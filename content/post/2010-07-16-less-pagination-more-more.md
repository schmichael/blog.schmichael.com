---
title: Less Pagination, More More
author: Michael Schurter
layout: post
date: 2010-07-17
url: /2010/07/16/less-pagination-more-more/
dsq_thread_id:
  - 463870984
categories:
  - SQL
  - Technology
tags:
  - cassandra
  - mongodb
  - urbanairship

---
We live in a brave new (to some) world of databases other than a relational database with a SQL interface. Normally end users never notice a difference, but the astute viewer may notice the slow demise of an old friend: pagination.

Traditionally with SQL databases pagination has looked something like this:
  
![][1]

There are previous and next links as well as links for jumping right to the beginning and end. Pretty boring stuff.

What&#8217;s interesting is that this standard interface is disappearing in favor of something like this:

_Twitter_
  
![][2]

_Facebook_
  
![][3]

And soon beta testers of [Urban Airship&#8217;s push service for Android][4] will see a More link on the page that lists devices associated with their app:

![][5]

The simplest possible explanation for this dumbing down of pagination is that **count (for total pages) and skip/offset are expensive operations.**

Not only are those operations expensive, but in eventually consistent databases, which many modern non-relational databases are, they&#8217;re extremely expensive, if not impossible, to perform.

**Cassandra**

At Urban Airship we, like Facebook, use [Cassandra][6]: a distributed column-based database. This deals two deadly blows to traditional pagination:

  1. No way to count columns in a row (without reading every column).
  2. No way to skip by numeric offset (so you can&#8217;t say, skip to page 5).

In Cassandra columns are ordered, so you start reading from the beginning and read N+1 columns where N is the number of items you&#8217;d like to display. The last column&#8217;s key is then used to determine whether the More link is enabled, and if so, what key to start the next &#8220;page&#8221; at. 

Both of those are solvable problems if you really need them, but I would suspect you would end up creating a column count cache as well as some sort of table of contents for the various page offsets. Not what I want to spend my time implementing.

The fact of the matter is that for many use cases, a simple More button works just as well (if not better) than traditional pagination. It&#8217;s also far cheaper to implement, which means more developer time free to work on features and more hardware resources available to push your 140 character insights around the web.

**MongoDB**

I should note that MongoDB is fairly unique in the non-relational database world as its dynamic querying features include [count][7] and [skip][8] operations. However, as with any database, you&#8217;ll want to make sure these queries hit indexes.

Sadly MongoDB currently doesn&#8217;t have the distributed features necessary to automatically handle data too big for a single server.

 [1]: http://schmichael.com/files/pagination.png
 [2]: http://schmichael.com/files/twitter-more.png
 [3]: http://schmichael.com/files/facebook-more.png
 [4]: http://blog.urbanairship.com/2010/05/25/android-delivers-push-notifications-are-here-to-stay/
 [5]: http://schmichael.com/files/apids-more.png
 [6]: http://cassandra.apache.org/
 [7]: http://www.mongodb.org/display/DOCS/Aggregation#Aggregation-Count
 [8]: http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries-%7B%7Bskip%28%29%7D%7D