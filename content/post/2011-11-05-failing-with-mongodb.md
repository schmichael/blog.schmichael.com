---
title: Failing with MongoDB
author: Michael Schurter
layout: post
date: 2011-11-05
url: /2011/11/05/failing-with-mongodb/
dsq_thread_id:
  - 463871018
categories:
  - Open Source
  - Technology
tags:
  - mongodb

---
**Update:** Sorry this isn&#8217;t my best piece of writing and there seems to be some confusion. The dataset in question was first in a 1.8 master/slave pair and then migrated to sharded replica sets and 2.0.0.

For a bit of history of my dealings with MongoDB at Urban Airship, I gave a couple versions of a Scaling with MongoDB talk:

  * [at Open Source Bridge (latest & greatest)][1] 
  * [at Update Portland (original, less polished version)][2]

My coworker Adam Lowry even gave a follow-up talk of sorts at [Postgres Open 2011][3] ([slides][4]) about migrating one of our datasets off of MongoDB and (back) on to PostgreSQL.

After reading through those slides you&#8217;re probably wondering why we&#8217;re still dealing with MongoDB at all. We fully intended to migrate our data out of it by now, but priorities change, deadlines slip, and we never expected one of our last uses of MongoDB to experience a surge in growth.

The dataset in question seemed ideal for MongoDB:

  * Ephemeral &#8211; if we lose it we experience service degradation for a short while, but nothing catastrophic
  * Small &#8211; easily fits into memory (~15 GB)
  * Secondary index &#8211; In a key/value store we would have had to manage a secondary index manually

So this dataset dodged a lot of the previous problems we had with MongoDB and seemed safe to migrate at our leisure.

<a name="global_write_lock"><b>Global Write Lock</b></a>

[MongoDB has a global write lock.][5] This means that while applying an insert or update, a single mongod instance can&#8217;t respond to other queries.

Our dataset may be small but it has a heavy read and write load. When the service it backed experienced a surge in usage, MongoDB quickly became CPU bound. This was especially frustrating considering mongod was running in a simple master/slave setup on two servers: each with 16 cores and enough memory to hold all the data a few times over again.

Because of the global write lock and heavy write load, operations are effectively serialized and executed on a single core. Meaning our servers didn&#8217;t even look loaded, as just 1 core would be 100% utilized by mongod.

<a name="sharding"><b>Let the Sharding Begin</b></a>

So we need to utilize multiple cores&#8230;
  
To do that we need multiple write locks&#8230;
  
There&#8217;s 1 write lock per mongod. So&#8230;
  
&#8230;multiple mongods per server?

We&#8217;d been avoiding sharding after having no luck getting it working in the 1.5.x dev series, but it&#8217;s our only choice now to get multiple mongods. I ran some tests and it seemed like we could turn our master/slave setup into a 2 shard setup with 2 mongods and 1 arbiter per shard with downtime in the seconds or low minutes.

The operational complexity of configuring a MongoDB cluster is daunting with each component bringing its own caveats:

**mongod config servers**

  * You need _exactly_ 3 config mongods (1 is fine for testing, which makes things appear simpler than they really are).
  * There are lots of caveats with the config servers, so read [Changing Config Servers][6] carefully before configuring your cluster.
  * Otherwise these mongod instances are fairly blackboxish to me. Despite being mongod processes you administer them completely differently.

**mongos routers**

  * 1 per app server. This wouldn&#8217;t be a big deal [except that our mongoses often start failing and require flushRouterConfig to be run on them][7]. [2.0.1 supposedly fixes this][8], but we haven&#8217;t tested that yet (and trading known problems for new unknown ones is always scary).
  * mongos instances can use a lot of CPU and seem to have random spikes where they fully utilize every core very briefly. Keep this in mind if your application servers are already CPU bound.
  * On the bright side mongos balanced our data rather quickly. Our shard key is a uuid, and it properly setup reasonable ranges in very short order without having to preconfigure them.
  * &#8220;mongos&#8221; is a terribly confusing name. It sounds like multiple mongo instances. We&#8217;ve taken to calling them mongooses internally due to frequent typos and confusion.

**arbiters**

  * You need at least 3 members in a replica set in order to complete an election if 1 member goes down.
  * We haven&#8217;t had any issues with arbiters&#8230; not sure what we&#8217;d do if one broke somehow but since they have no persistent data they&#8217;re safe to restart at any time.

**mongods**

  * Early on we ran into a problem where changing replica set member entries wasn&#8217;t propagated to the config servers&#8217; shard configuration. Restarting every mongos fixed it.
  * As far as I can tell a new replica set member will never leave the initial RECOVERING state until all operations to that set are stopped. Even 40 updates per second was enough of a trickle to prevent a new set member from leaving RECOVERING to becoming a SECONDARY. We had to shutdown mongoses to cut off all traffic to bring up a new member. (The replication log gave every indication of being caught up and our usual update load is thousands per second.)
  * Setting rest in the config file doesn&#8217;t seem to work. Put &#8211;rest in your command line options.
  * Sending an HTTP request to a mongod&#8217;s main port (instead of the HTTP endpoint) seems to be capable of crashing the mongod.

**Client Drivers**

While a single replica set member was in a RECOVERING state our Java services couldn&#8217;t complete _any_ operations while our Python service was happily working away.

**Summary**

Right now we&#8217;re getting by with 2 shards on 2 dedicated servers and then mongoses and config servers spread throughout other servers. There appears to be some data loss occurring, though due to the ephemeral fast changing nature of this dataset it&#8217;s very difficult to determine definitively or reproduce independently.

So we&#8217;re trying to migrate off of MongoDB to a custom service better suited for this dataset ASAP.

 [1]: http://opensourcebridge.org/2011/wiki/Scaling_with_MongoDB
 [2]: /2011/02/02/schmongodb-slides-from-update-portland/
 [3]: http://postgresopen.org/2011/schedule/presentations/98/
 [4]: http://wiki.postgresql.org/images/7/7f/Adam-lowry-postgresopen2011.pdf
 [5]: http://www.mongodb.org/display/DOCS/How+does+concurrency+work#Howdoesconcurrencywork-Read%2FWriteLock
 [6]: http://www.mongodb.org/display/DOCS/Changing+Config+Servers
 [7]: http://www.mongodb.org/display/DOCS/flushRouterConfig+command
 [8]: https://jira.mongodb.org/browse/SERVER-3739