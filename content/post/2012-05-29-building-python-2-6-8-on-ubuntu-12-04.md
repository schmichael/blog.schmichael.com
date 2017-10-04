---
title: Building Python 2.6.8 on Ubuntu 12.04
author: Michael Schurter
layout: post
date: 2012-05-29
url: /2012/05/29/building-python-2-6-8-on-ubuntu-12-04/
dsq_thread_id:
  - 707640786
categories:
  - GNU/Linux
  - Open Source
  - Python

---
**Update 2012-06-01:** Looks like [pythonz][1] is an easier way to install Python 2.6.8 (and all other Pythons) on Ubuntu 12.04.

Ubuntu 12.04 builds OpenSSL without SSLv2. Python 2.6.8 expects OpenSSL to be built with SSLv2.

[This is a bug that has been fixed in Python 2.7+][2], but it wasn&#8217;t backported for Python 2.6.

So if you build your own Python 2.6 binaries on Ubuntu 12.04 you&#8217;ll see errors like this when attempting to use anything SSL related:

`*** WARNING: renaming "_ssl" since importing it failed: build/lib.linux-x86_64-2.6/_ssl.so: undefined symbol: SSLv2_method`

Some of us still need Python 2.6, so [I forked Python 2.6.8 and removed SSLv2 support][3]. Tests pass and SSL works.

You can also just grab the diff below:



**Update:** M2Crypto requires patching as well: 

**Update 2:** If you trust me and use 64bit Ubuntu 12.04 you can download a pre-built [python-2.6.8~nosslv2][4] tarball from me. Includes distribute and pip pre-installed.

 [1]: https://github.com/saghul/pythonz
 [2]: http://bugs.python.org/issue12012
 [3]: https://bitbucket.org/schmichael/cpython-v2.6.8-nosslv2/src/d77684a8fdd5
 [4]: https://schmichael.com/files/python-2.6.8~nosslv2.tar.gz