---
title: Drupal Database Maintenance Script
author: Michael Schurter
layout: post
date: 2007-08-03
url: /2007/08/03/drupal-database-maintenance-script/
dsq_thread_id:
  - 463870500
categories:
  - GNU/Linux
  - Open Source
  - PHP
  - SQL
  - Technology

---
I love [Drupal][1], but its insistence on saving every session its ever created causes the `sessions` table to become massive. So I usually end up creating a shell script like the following:

**drupal-db-maint.sh** (I posted [a copy to pastebin][2] since WordPress makes the code impossible to read.)

<div style="border: 1px solid #cccccc; margin: 2px; padding: 2px; font-family: monospace; font-size: 8pt; text-align: left">
  #!/bin/sh<br /> echo `date` &#8211; Starting Drupal database maintenance<br /> MYSQL_USERNAME=&#8217;<strong>insert your MySQL username here</strong>&#8216;<br /> MYSQL_PASSWORD=&#8217;<strong>insert your MySQL password here</strong>&#8216;<br /> MYSQL_DATABASE=&#8217;<strong>insert your database name here</strong>&#8216;</p> 
  
  <p>
    # Note: 2592000 = sessions over 30 days old.<br /> # Adjust the timespan as desired.<br /> CLEAN_SESSIONS_SQL=&#8217;DELETE FROM `sessions` WHERE `timestamp` < (UNIX_TIMESTAMP() &#8211; 2592000)&#8217;<br /> OPTIMIZE_CACHES_SQL=&#8217;OPTIMIZE TABLE `cache` , `cache_filter` , `cache_menu` , `cache_page` , `cache_views` , `sessions`&#8217;
  </p>
  
  <p>
    # Note: I have tons of modules installed.<br /> # I tried cleaning out their table names before posting, but you&#8217;ll want to double check this SQL.<br /> OPTIMIZE_REST_SQL=&#8217;OPTIMIZE TABLE `access` , `accesslog` , `aggregator_category` , `aggregator_category_feed` , `aggregator_category_item` , `aggregator_feed` , `aggregator_item` , `authmap` , `blocks` , `blocks_roles` , `boxes` , `client` , `client_system` , `comments` , `contact` , `files` , `file_revisions` , `filters` , `filter_formats` , `flood` , `history` , `invite` , `menu` , `node` , `node_access` , `node_comment_statistics` , `node_counter` , `node_revisions` , `node_type` , `permission` , `profile_fields` , `profile_values` , `role` , `search_dataset` , `search_index` , `search_total` , `sequences` , `system` , `term_data` , `term_hierarchy` , `term_node` , `term_relation` , `term_synonym` , `url_alias` , `users` , `users_roles` , `variable` , `vocabulary` , `vocabulary_node_types` , `watchdog`&#8217;
  </p>
  
  <p>
    # Note: I run this script on a Linode which has limited IO.<br /> # Adding a short wait between commands lessens the load on the server.<br /> SLEEP_TIME=5
  </p>
  
  <p>
    echo $CLEAN_SESSIONS_SQL | mysql -u $MYSQL_USERNAME -p$MYSQL_PASSWORD $MYSQL_DATABASE<br /> sleep $SLEEP_TIME
  </p>
  
  <p>
    echo $OPTIMIZE_CACHES_SQL | mysql -u $MYSQL_USERNAME -p$MYSQL_PASSWORD $MYSQL_DATABASE > /dev/null<br /> sleep $SLEEP_TIME
  </p>
  
  <p>
    echo $OPTIMIZE_REST_SQL | mysql -u $MYSQL_USERNAME -p$MYSQL_PASSWORD $MYSQL_DATABASE > /dev/null
  </p>
  
  <p>
    echo `date` &#8211; Done with Drupal database maintenance
  </p>
</div>

Then just run `crontab -e` to edit your crontab and add a line similar to:
  
`46  4  *   *   *     /path/to/drupal-db-maint.sh`

That will optimize your database nightly at 4:46 AM server time (usually UTC).

If you don&#8217;t like my solution, there are plenty of [more elegant session cleaning solutions out there][3]. I&#8217;m just more comfortable writing shell scripts and crontabs than Drupal modules that use [hook_cron][4].

<small>Posting code in WordPress so that its readable is pretty much impossible. Any suggestions?</small>

 [1]: http://drupal.org
 [2]: http://pastebin.ca/644472
 [3]: http://tools.ourmedia.org/blog/markus_sandy/performance_and_a_new_module
 [4]: http://api.drupal.org/api/function/hook_cron/5