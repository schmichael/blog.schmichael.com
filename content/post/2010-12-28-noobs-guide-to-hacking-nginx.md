---
title: A Complete Noobs Guide to Hacking Nginx
author: Michael Schurter
layout: post
date: 2010-12-29
url: /2010/12/28/noobs-guide-to-hacking-nginx/
dsq_thread_id:
  - 463870998
categories:
  - Open Source
  - Technology
tags:
  - c
  - eclipse
  - gdb
  - nginx

---
At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

```At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

``` 

Note that I set the prefix to a path in my home directory, turned on debugging and the dav module, and set nginx to run as my user and group. A quick symlink from /home/schmichael/local/nginx/sbin/nginx to ~/bin/nginx, and I can start and restart nginx quickly and easily. More importantly I can attach a debugger to it.

The importance of being able to attach a debugger became clear as soon as I tested [dav support (with their standard config)][14]:
  
````At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

```At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

``` 

Note that I set the prefix to a path in my home directory, turned on debugging and the dav module, and set nginx to run as my user and group. A quick symlink from /home/schmichael/local/nginx/sbin/nginx to ~/bin/nginx, and I can start and restart nginx quickly and easily. More importantly I can attach a debugger to it.

The importance of being able to attach a debugger became clear as soon as I tested [dav support (with their standard config)][14]:
  
```` 

My patch was causing a segfault in the dav module that killed nginx's worker process. Bumping up my error logging to `debug` level didn't give me many clues:
  
`````At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

```At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

``` 

Note that I set the prefix to a path in my home directory, turned on debugging and the dav module, and set nginx to run as my user and group. A quick symlink from /home/schmichael/local/nginx/sbin/nginx to ~/bin/nginx, and I can start and restart nginx quickly and easily. More importantly I can attach a debugger to it.

The importance of being able to attach a debugger became clear as soon as I tested [dav support (with their standard config)][14]:
  
````At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

```At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

``At [Urban Airship][1] our [RESTful HTTP API][2] uses PUT requests for, among other things, [registering a device][3]. Since the application registering the device is the HTTP Basic Auth username, there&#8217;s often no body ([entity body][4] in HTTP parlance). Unfortunately [nginx][5] (as of 0.8.54, and I believe 0.9.3) doesn&#8217;t support PUT requests without a Content-Length header and responds with a 411 Length Required response. While the [chunkin][6] module adds Transfer-Encoding: chunked support, it doesn&#8217;t fix the empty PUT problem since HTTP requests without bodies don&#8217;t require Content-Length nor Transfer-Encoding headers.

So let&#8217;s hack nginx shall we?

I know a bit of C but am primarily a Python developer, so hacking an established C project doesn&#8217;t come easily to me. To make matters worse, as far as I can tell there&#8217;s no official public source repository ([but there&#8217;s a mirror][7]) and it seems to be mainly developed by the creator, [Igor Sysoev][8]. At least the code looks clean.

**First Pass**

I had [nginx-0.8.54.tar.gz][9] handy from compiling the source and nginx was nice enough to log an error for PUTs without Content-Length:

> client sent PUT method without &#8220;Content-Length&#8221; header while reading client request headers, client: &#8230;, server: , request: &#8220;PUT / HTTP/1.1&#8221; &#8230; 

So let&#8217;s use [ack][10] to find it:

![ack-grep 'client sent .* method without'][11]

A quick `vim +1532 src/http/ngx_http_request.c` later and we&#8217;re looking at the problem:

<pre lang="c">if (r->method &#038; NGX_HTTP_PUT &#038;&#038; r->headers_in.content_length_n == -1) {
        ngx_log_error(NGX_LOG_INFO, r->connection->log, 0,
                  "client sent %V method without \"Content-Length\" header",
                  &#038;r->method_name);
        ngx_http_finalize_request(r, NGX_HTTP_LENGTH_REQUIRED);
        return NGX_ERROR;
    }</pre>

This code returns the 411 Length Required response for PUTs lacking a Content-Length header. Remove it, recompile (`make -j2 &#038;&#038; sudo make install &#038;&#038; sudo service nginx restart`), and test:

`` 

Success! Now create a patch `diff -ru nginx-0.8.54 nginx > fix-empty-put.patch` and [post it to the nginx-devel mailing list][12].

Now to play Minecraft for 12 hours as you wait for the Russian developers to wake up and take notice of your patch. Possibly sleep.

**Second Pass: Fixing WebDAV**

A positive [reply from Maxim Dounin to my patch][13]! I don't use WebDAV though, but if I want this patch accepted I better make sure it doesn't break official modules.

This time around I wanted to work locally, so I installed nginx with the following configuration:

``` 

Note that I set the prefix to a path in my home directory, turned on debugging and the dav module, and set nginx to run as my user and group. A quick symlink from /home/schmichael/local/nginx/sbin/nginx to ~/bin/nginx, and I can start and restart nginx quickly and easily. More importantly I can attach a debugger to it.

The importance of being able to attach a debugger became clear as soon as I tested [dav support (with their standard config)][14]:
  
```` 

My patch was causing a segfault in the dav module that killed nginx's worker process. Bumping up my error logging to `debug` level didn't give me many clues:
  
````` 

Time to break out the debugger! While I've used `gdb --pid` to attach to running processes before, I'd just installed Eclipse to work on some Java code and wondered if it might make debugging a bit easier.

After installing plugins for C/C++, Autotools, and GDB, I could easily import nginx by creating a "New Makefile project with existing code":
  
![Import existing code][15]

Now create a new Debug Configuration:
  
![Debug Configuration][16]

_**Note** on Linux systems (at least Ubuntu):_ by default PTRACE is disabled in the kernel. Just flip the 1 to 0 in `/etc/sysctl.d/10-ptrace.conf` and run `sudo sysctl -p /etc/sysctl.d/10-ptrace.conf` to allow PTRACE.

Finally click "Debug" and select the nginx _worker_ process from your process list:
  
![Select Process][17]

By default GDB will pause the process it attaches to, so make sure to click the Resume button (or press F8) to allow nginx to continue serving requests.

**Crashing nginx**
  
Now cause the segfault by running our curl command `curl -v -X PUT http://localhost:8888/foo`. This time curl won't return because gdb/Eclipse caught the segfault in the nginx child process, leaving the socket to curl open. A quick peek in Eclipse shows us exactly where the segfault occurs:
  
![Debugging in Eclipse][18]

Eclipse makes it quick and easy to interactively inspect the variables. Doing that I discovered the culprit was the src variable being uninitialized. Bouncing up the stack once you can see dav's put handler expects to be given a temporary file (`&#038;r->request_body->temp_file->file.name`) full of PUT data (of which we sent none), and it copies that to the destination file (`path`).

Bounce up the stack again to `ngx_http_read_client_request_body` and you can see this relevant code:

<pre lang="c">if (r->headers_in.content_length_n &lt; 0) {</pre>

nginx's core HTTP module short circuits a bit when there's no Content-Length specified. It skips the temp file creation because there's no data to put into the temp file!

So we have our problem:

  1. The dav module put handler expects a temp file containing the data to be saved.
  2. The http module doesn't create a temp file when there's no body data.

The 2 solutions I can think of are:

  1. Always create a temp file, even if it's empty.
  2. Add a special case to the dav module's put handler for when the temp file doesn't exist.

I really don't want to hack the core http module just to make a sub-module happy. It _makes sense_ that no temporary file exists when there's no body data. Sub-modules shouldn't be lazy and expect it to exist. So I decided to try #2.

**The Fix**

You can see my [implementation of solution #2 on GitHub][19]. Simply put, if the temp file exists, follow the existing logic. If the temp file does not exist we have a PUT with an empty body: use nginx's open wrapper to do a create or truncate (`O_CREAT|O_TRUNC`) on the destination file (since an empty PUT should create an empty file).

I don't know if this is the best solution or even a correct one, but it appears to work and was a fun journey arriving at it. You can [follow the discussion on the mailing list][20].

<small>Updated to switch from bitbucket to github.</small>

 [1]: http://urbanairship.com
 [2]: http://en.wikipedia.org/wiki/Representational_State_Transfer#RESTful_web_services
 [3]: http://urbanairship.com/docs/push.html#registration
 [4]: http://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html#sec7.2
 [5]: http://wiki.nginx.org
 [6]: http://wiki.nginx.org/HttpChunkinModule
 [7]: https://github.com/git-mirror/nginx
 [8]: http://sysoev.ru/en/
 [9]: http://nginx.org/download/nginx-0.8.54.tar.gz
 [10]: http://betterthangrep.com/
 [11]: http://schmichael.com/files/nginx-01-ack.png "ack-grep 'client sent .* method without'"
 [12]: http://nginx.org/pipermail/nginx-devel/2010-December/000605.html
 [13]: http://nginx.org/pipermail/nginx-devel/2010-December/000606.html
 [14]: http://wiki.nginx.org/HttpDavModule
 [15]: http://schmichael.com/files/nginx-02-import-existing.png
 [16]: http://schmichael.com/files/nginx-03-debug-conf.png
 [17]: http://schmichael.com/files/nginx-04-select-process.png
 [18]: http://schmichael.com/files/nginx-05-debugging.png
 [19]: https://github.com/schmichael/nginx/commit/c6051556460561bac4b0931fd9436e37b84925a3
 [20]: http://nginx.org/pipermail/nginx-devel/2010-December/000609.html