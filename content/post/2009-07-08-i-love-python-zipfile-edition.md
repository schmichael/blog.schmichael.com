---
title: 'I Love Python: ZipFile Edition'
author: Michael Schurter
layout: post
date: 2009-07-08
url: /2009/07/08/i-love-python-zipfile-edition/
dsq_thread_id:
  - 463870916
categories:
  - Open Source
  - Python
  - Technology
tags:
  - django
  - zip

---
For a client web project I needed to create a zip file containing a number of generated XML files. This isn&#8217;t something I need to do very often, so I briefly considered just writing the XML files to disk and running a zip command. Ugly, but surely trying to dig up a pleasant Python zip library would be more work?

Turns out Python has had a wonderful zip library in its standard library since 1.6! The `<a href="http://docs.python.org/library/zipfile.html">zipfile</a>` module makes creating zip files a breeze:

<pre lang="python">import os
from zipfile import ZipFile, ZIP_DEFLATED

from django.template.defaultfilters import slugify

from somewhere_else import render_spam_xml, render_egg_xml

ZIP_PATH = "/some/system/path/for/zips"

def create_zip(spam):
    spam_slug = slugify(spam.name)
    filename = "%s.zip" % spam_slug
    abspath = os.path.join(ZIP_PATH, filename)

    # Create zip
    z = ZipFile(abspath, "w", ZIP_DEFLATED)

    # Write spam xml directly to zip
    z.writestr("%s.xml" % spam_slug, render_spam_xml(spam))

    # Write xml files to zip
    for egg in spam.egg_set.all():
        egg_slug = slugify(egg.name)

        # Renders the egg object to an xml string
        xml = render_egg_xml(egg)

        # Note how easy it is to specify paths in the zip file:
        z.writestr("eggs/%s.xml" % egg_slug, xml)

    # Zip file must be closed to be valid
    z.close()
    return abspath
</pre>

<small>(Sorry for the Django bits in there, but they should be easy to replace.)</small>

My favorite part is that you can use either the `ZipFile.write` method to add files to the zip or the `ZipFile.writestr` method to write bytes (strings in my case) directly to the zip file.

At any rate, just wanted to blog about it, so when I need to do it again in a few years I don&#8217;t do something stupid like running the zip command.