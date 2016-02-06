---
title: eval() is evil too
author: Michael Schurter
layout: post
date: 2005-08-15
url: /2005/08/15/eval-is-evil-too/
dsq_thread_id:
  - 463869741
categories:
  - PHP

---
[This][1] is the most beautiful changelog entry a PHP project can have: `eliminate use of eval().` Evidently the [XML-RPC PEAR package][2] has managed to remove every last vestigate of the horrific [eval()][3] function.

Congratulations to the XML-RPC PEAR package maintainers for this excellent improvement!

 [1]: http://pear.php.net/package/XML_RPC/download/1.4.0/
 [2]: http://pear.php.net/package/XML_RPC/
 [3]: http://us3.php.net/eval