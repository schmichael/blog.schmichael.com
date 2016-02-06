---
title: Making Server-Side MongoDB Functions Less Awkward
author: Michael Schurter
layout: post
date: 2010-01-12
url: /2010/01/11/making-server-side-mongodb-functions-less-awkward/
dsq_thread_id:
  - 463903092
categories:
  - Open Source
  - Python
  - Technology
tags:
  - javascript
  - mongodb
  - pymongo

---
I&#8217;ve recently switched my project at work to use MongoDB for the user database and a few other datasets.

Currently I don&#8217;t use many JavaScript functions, but when I do I like to store them on the server so that they&#8217;re accessible when I&#8217;m poking around in a console.

I use something similar to the following function to load all of my JS functions onto the server when my app starts:

<pre lang="python">import os
import pymongo
import pkg_resources

# Relative to distribution's root
SCRIPT_DIR = os.path.join('model', 'js')

def init_js(db):
    '''Initializes server-side javascript functions'''
    scripts = filter(
            lambda f: f.endswith('.js'),
            pkg_resources.resource_listdir(__name__, SCRIPT_DIR)
        )
    for script in scripts:
        # Name the function after the script name
        func_name, _ = script.split('.', 1)
        script_path = os.path.join(SCRIPT_DIR, script)

        # Create a pymongo Code object
        # otherwise it will be stored as a string
        code = pymongo.code.Code(
                pkg_resources.resource_string(__name__, script_path))

        # Upsert the function
        db.system.js.save({ '_id': func_name, 'value': code, })
</pre>

However, using server-side functions from Python is awkward at best. Say I have the JavaScript function:

**add.js**

<pre lang="javascript">function(x, y) {
    return x + y;
}
</pre>

To run that function via PyMongo requires wrapping the function call with placeholder parameters in a Code object and passing in values as a dict:

<pre lang="python">var1 = 1
var2 = 2
result = db.eval(pymongo.code.Code('add(a, b)', {'a': var1, 'b': var2,}))
assert result == 3
</pre>

**Update:** See [MongoDB dev Mike Dirolf comment][1] to see a much more concise way of executing server-side functions.

Bearable for simple functions, but having to manually map parameters to values is tiresome and error prone with longer function signatures.

What I wanted was something more natural like:

<pre lang="python">var1 = 1
var2 = 2
result = db.add(var1, var2)
assert result == 3
</pre>

I use a simple PyMongo Database object wrapper to make my life easier:

<pre lang="python">import string

from pymongo.code import Code

class ServerSideFunctions(object):
    def __init__(self, db):
        self.db = db

    def func_wrapper(self, func):
        '''Returns a closure for calling a server-side function.'''
        params = [] # To keep params ordered
        kwargs = {}
        def server_side_func(*args):
            '''Calls server side function with positional arguments.'''
            # Could be removed with better param generating logic
            if len(args) > len(string.letters):
                raise TypeError('%s() takes at most %d arguments (%d given)'
                        % (func, len(string.letters), len(args)))
            
            # Prepare arguments
            for k, v in zip(string.letters, args):
                kwargs[k] = v
                params.append(k) 

            # Prepare code object
            code = Code('%s(%s)' % (func, ', '.join(params)), kwargs)
                
            # Return result of server-side function
            return self.db.eval(code)
        return server_side_func

    def __getattr__(self, func):
        '''Return a closure for calling server-side function named `func`'''
        return self.func_wrapper(func)

dbjs = ServerSideFunctions('foo')
var1 = 1
var2 = 2
result = dbjs.add(var1, var2)
assert result == 3
</pre>

I&#8217;m tempted to monkey-patch PyMongo&#8217;s Database class to add a ServerSideFunctions instance directly as a js attribute, so then I could drop the confusing `dbjs` variable and just use:

<pre lang="python">assert db.js.add(1,2) == 3
</pre>

If someone knows of a better way to access server-side MongoDB functions from Python, please let me know!

<small>I modified this code to remove code specific to my project, so please let me know if there are errors.</small>

 [1]: http://michael.susens-schurter.com/blog/2010/01/11/making-server-side-mongodb-functions-less-awkward/comment-page-1/#comment-68027