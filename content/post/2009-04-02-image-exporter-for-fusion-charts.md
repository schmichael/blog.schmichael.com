---
title: Image Exporter for Fusion Charts
author: Michael Schurter
layout: post
date: 2009-04-02
url: /2009/04/02/image-exporter-for-fusion-charts/
dsq_thread_id:
  - 463870888
categories:
  - Open Source
  - Python
  - Technology
tags:
  - fusioncharts
  - pil

---
I wrote an image exporter for [Fusion Charts][1] while working for [YouGov/Polimetrix][2], and someone recently asked if they could use it as well.

You&#8217;ll have to alter it a bit because it was written for a custom [CherryPy][3]-based framework. It works with Fusion Charts 3.1 (and 3.0 with trivial changes to the POST variables being read).

The only dependency is on [PIL][4]:

<pre lang="python">from StringIO import StringIO
import Image
import ImageColor

import cherrypy

def str2color(val):
    return ImageColor.getrgb('#'+val.ljust(6, '0'))

class SaveImagePage(LoggedInPage):  # Custom framework specific -- remove
    def control(self, page, meta_width='', meta_height='', meta_bgColor='ffffff', stream=''):
        # Convert 3.1 parameters to 3.0 style as they made more sense
        width = meta_width
        height = meta_height
        bgcolor = meta_bgColor
        data = stream

        # Split the data into rows using ; as the spearator
        rows = data.split(';')

        # Create image
        bgcolor = str2color(bgcolor)
        im = Image.new('RGB', (int(width), int(height)), bgcolor)
        imcore = im.load()

        for y, row in enumerate(rows):
            x = 0

            # Split row into pixels
            pixels = row.split(',')
            for pixel in pixels:
                # Split pixel into color and repeat value
                color, repeat = pixel.split('_')
                repeat = int(repeat)

                if color == '':
                    # Empty color == background color
                    color = bgcolor
                else:
                    # Pad color to 6 characters
                    color = str2color(color)

                while repeat:
                    # Add pixels 1-at-a-time since putdata() doesn't work
                    imcore[x, y] = color
                    x += 1
                    repeat -= 1

        # Save image into file like object
        imstr = StringIO()
        im.save(imstr, 'PNG', quality=100)

        # Set HTTP headers -- CherryPy specific code
        cherrypy.response.headers['content-type'] = 'image/png'
        cherrypy.response.headers['content-disposition'] = \
                'attachment; filename="Chart.png'

        # Return image as string, your framework may be different
        return imstr.getvalue()
</pre>

 [1]: http://www.fusioncharts.com/
 [2]: http://www.polimetrix.com/
 [3]: http://cherrypy.org
 [4]: http://www.pythonware.com/products/pil/