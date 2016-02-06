---
title: Sharing Python data between processes using mmap
author: Michael Schurter
layout: post
date: 2011-05-16
url: /2011/05/15/sharing-python-data-between-processes-using-mmap/
dsq_thread_id:
  - 463968912
categories:
  - GNU/Linux
  - Open Source
  - Python
  - Technology
tags:
  - ctypes
  - mmap
  - Python
  - struct

---
I&#8217;ve been toying with an idea of exposing statistics for a Python application via shared memory to keep the performance impact on the application as low as possible. The goal being an application could passively expose a number of metrics that could either be periodically polled via [munin][1]/[Icinga][2]/etc plugins or interactive tools when diagnosing issues on a system.

But first things first: I need to put data into [shared memory][3] from Python. [mmap][4] is an excellent widely-implemented POSIX system call for creating a shared memory space backed by an on-disk file.

Usually in the UNIX world you have 2 ways of accessing/manipulating data: memory addresses or streams (files). Manipulating data via memory addresses means [pointers][5], offsets, [malloc/free][6], etc. Stream interfaces manipulate data via [read/write/seek system calls][7] for files and [send/recv/etc for sockets][8].

mmap gives you both interfaces. A memory mapped file can be manipulated via read/write/seek or by directly accessing its mapped memory region. The advantage of the latter is that this memory region is in userspace &#8212; meaning you can manipulate a file without incurring the overhead of write system calls for every manipulation.

Anyway, enough exposition, let&#8217;s see some code. <small>(Despite mmap&#8217;s nice featureset, I&#8217;m only using it as a simple memory sharing mechanism anyway.)</small> The following code shares a tiny bit of data between 2 Python processes using the excellent [mmap module in the stdlib][9]. `a.py` writes to the memory mapped region, and `b.py` reads the data out. [ctypes][10] allows for an easy way to create values in a memory mapped region and manipulate them like &#8220;normal&#8221; Python objects.

_These code samples were written using Python 2.7 on Linux. They should work fine on any POSIX system, but Windows users will have to change the mmap calls to match the Windows API._

**a.py**

<pre lang="python">#!/usr/bin/env python
import ctypes
import mmap
import os
import struct


def main():
    # Create new empty file to back memory map on disk
    fd = os.open('/tmp/mmaptest', os.O_CREAT | os.O_TRUNC | os.O_RDWR)

    # Zero out the file to insure it's the right size
    assert os.write(fd, '\x00' * mmap.PAGESIZE) == mmap.PAGESIZE

    # Create the mmap instace with the following params:
    # fd: File descriptor which backs the mapping or -1 for anonymous mapping
    # length: Must in multiples of PAGESIZE (usually 4 KB)
    # flags: MAP_SHARED means other processes can share this mmap
    # prot: PROT_WRITE means this process can write to this mmap
    buf = mmap.mmap(fd, mmap.PAGESIZE, mmap.MAP_SHARED, mmap.PROT_WRITE)

    # Now create an int in the memory mapping
    i = ctypes.c_int.from_buffer(buf)

    # Set a value
    i.value = 10

    # And manipulate it for kicks
    i.value += 1
    
    assert i.value == 11

    # Before we create a new value, we need to find the offset of the next free
    # memory address within the mmap
    offset = struct.calcsize(i._type_)

    # The offset should be uninitialized ('\x00')
    assert buf[offset] == '\x00'

    # Now ceate a string containing 'foo' by first creating a c_char array
    s_type = ctypes.c_char * len('foo')

    # Now create the ctypes instance
    s = s_type.from_buffer(buf, offset)

    # And finally set it
    s.raw = 'foo'

    print 'First 10 bytes of memory mapping: %r' % buf[:10]
    raw_input('Now run b.py and press ENTER')

    print
    print 'Changing i'
    i.value *= i.value

    print 'Changing s'
    s.raw = 'bar'

    new_i = raw_input('Enter a new value for i: ')
    i.value = int(new_i)


if __name__ == '__main__':
    main()
</pre>

**b.py**

<pre lang="python">import mmap
import os
import struct
import time

def main():
    # Open the file for reading
    fd = os.open('/tmp/mmaptest', os.O_RDONLY)

    # Memory map the file
    buf = mmap.mmap(fd, mmap.PAGESIZE, mmap.MAP_SHARED, mmap.PROT_READ)

    i = None
    s = None

    while 1:
        new_i, = struct.unpack('i', buf[:4])
        new_s, = struct.unpack('3s', buf[4:7])

        if i != new_i or s != new_s:
            print 'i: %s => %d' % (i, new_i)
            print 's: %s => %s' % (s, new_s)
            print 'Press Ctrl-C to exit'
            i = new_i
            s = new_s

        time.sleep(1)


if __name__ == '__main__':
    main()
</pre>

<small>(Note that I cruelly don&#8217;t clean up /tmp/mmaptest after the scripts finished. Consider it a 4KB tax for anyone who runs arbitrary code they found on the Internet without reading it first.)</small>

 [1]: http://munin-monitoring.org/
 [2]: http://www.icinga.org/
 [3]: http://en.wikipedia.org/wiki/Shared_memory
 [4]: http://en.wikipedia.org/wiki/Mmap
 [5]: http://en.wikipedia.org/wiki/Pointer_%28computing%29
 [6]: http://en.wikipedia.org/wiki/Malloc
 [7]: http://en.wikipedia.org/wiki/System_call
 [8]: http://en.wikipedia.org/wiki/Berkeley_sockets
 [9]: http://docs.python.org/library/mmap
 [10]: http://docs.python.org/library/ctypes