---
title: OpenIT has a demo site!
author: Michael Schurter
layout: post
date: 2005-11-02
url: /2005/11/02/openit-has-a-demo-site/
dsq_thread_id:
  - 530719131
categories:
  - Open Source
tags:
  - OpenIT

---
I finally got around to setting up a [demo site][1] for [OpenIT][2] over on SourceForge.

Not very much hacking was required. I actually fixed a couple bugs in tools/setup.php because of the experience. I had to add `define('DB_DATAOBJECT_NO_OVERLOAD',true);` to the top of the file `inc/pear/DB/DataObject.php`, and add `session_save_path('/tmp/persistent');` to the top of `inc/common.php`.

I guess I should get around to posting the good news on the [I finally got around to setting up a [demo site][1] for [OpenIT][2] over on SourceForge.

Not very much hacking was required. I actually fixed a couple bugs in tools/setup.php because of the experience. I had to add `define('DB_DATAOBJECT_NO_OVERLOAD',true);` to the top of the file `inc/pear/DB/DataObject.php`, and add `session_save_path('/tmp/persistent');` to the top of `inc/common.php`.

I guess I should get around to posting the good news on the][3] [community home page.][2]

 [1]: http://openit.sourceforge.net/openit/
 [2]: http://openit.synthesyssolutions.com/
 [3]: https://sourceforge.net/projects/openit