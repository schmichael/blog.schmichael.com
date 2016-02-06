---
title: Debugging Go 1.2 on Ubuntu 13.10 with GDB
author: Michael Schurter
layout: post
date: 2014-04-02
url: /2014/04/02/debugging-go-1-2-on-ubuntu-13-10-with-gdb/
dsq_thread_id:
  - 2581729212
categories:
  - Uncategorized
tags:
  - debugging
  - gdb
  - golang
  - ubuntu

---
While the [Debugging Go Code with GDB][1] documentation is fantastic, it unfortunately doesn&#8217;t work out of the box with Ubuntu 13.10. If you try it you&#8217;ll probably see an error similar to:



The problem is that Ubuntu 13.10 links GDB against Python 3.3 while the script golang ships is for Python 2. [Someone has already filed an issue, and it appears to be fixed][2] upstream (so expect Go 1.3 to Just Work).

Luckily backporting the fix is easy. Simply move your existing `runtime-gdb.py` out of the way and [download the upstream version][3] in its place.

If your `$GOROOT` is `/usr/local/go` the following should Just Work:

 [1]: http://golang.org/doc/gdb
 [2]: https://code.google.com/p/go/issues/detail?id=6698
 [3]: https://go.googlecode.com/hg/src/pkg/runtime/runtime-gdb.py