---
title: Iconoclastic Computer
author: Michael Schurter
layout: post
date: 2005-08-24
url: /2005/08/24/when-windows-games-attack/
dsq_thread_id:
  - 555339344
categories:
  - IT
tags:
  - Synthesys

---
This is weird &#8212; one of the users at a company I consult at came to me with a problem this morning: some of his Adobe Illustrator 11 documents had their icons mysteriously changed overnight. This guy is a star user too. He doesn&#8217;t get spyware, he doesn&#8217;t mess around, he just wants a computer that works.

But sure enough, some of his Illustrator documents **had the icons from games in Windows XP**. Each document had a different game icon.

After manually setting the icon in the hideous File Types tab, deleting the infamous IconCache.db file, and restarting the problem persisted. So then I **renamed the files, and their icons went back to normal!** Renaming them back changed the icon back into the game icon.

I haven&#8217;t dug around the [Microsoft KnowledgeBase][1] yet, but this is really strange. Of course [SpyBot][2] and McAfee Antivirus are running as I type &#8230; but so far everything checks out &#8230; weird &#8230;

**Update:** [Aaron][3] gave me the new and completely appropriate name for this post. And for the record, turning Thumbnail caching on and off fixed almost all of the icons. Somehow one of them still uses the icon for Internet Hearts or something&#8230;

 [1]: http://support.microsoft.com/default.aspx?scid=FH;EN-US;KBHOWTO
 [2]: http://www.spybot.info/
 [3]: http://blogs.synthesyssolutions.com/aaron/