---
title: MemoryMapFile Convenience Class for Python
author: Michael Schurter
layout: post
date: 2011-09-06
url: /2011/09/05/memorymapfile-convenience-class-for-python/
dsq_thread_id:
  - 463968370
categories:
  - Open Source
  - Python
  - Technology
tags:
  - mmap

---
My [obsession][1] with [mmap][2] hasn&#8217;t died, but while [Python&#8217;s mmap module][3] is a wonderful low level library it&#8217;s a bit hard for a newcomer to use properly.

I&#8217;ve started toying with a convenience wrapper class for `mmap.mmap` (at least the Unix version):
  


My original goal was to automatically [grow][4] the mmap whenever the user attempts to write beyond the current size of the mmap file, but that&#8217;s going to take carefully wrapping quite a few methods (`write`, `__setitem__`, and maybe get/read methods too).

If it becomes useful, I may use it in [mmstats][5].

Feedback welcome!

**Update:** Discovered the hard way (segfaults) that resizing mmaps is tricky: the region can be moved but data will be copied. However, any existing pointers (from ctypes.<type>.from_buffer in my case) will now point to freed memory and segfault upon use.

tl;dr &#8211; If at all possible, precompute the size of your mmap before using it.

 [1]: /2011/05/15/sharing-python-data-between-processes-using-mmap/
 [2]: http://en.wikipedia.org/wiki/Mmap
 [3]: http://docs.python.org/library/mmap
 [4]: http://docs.python.org/library/mmap#mmap.resize
 [5]: https://github.com/schmichael/mmstats