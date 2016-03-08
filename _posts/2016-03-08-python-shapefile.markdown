---
layout: post
comments: true
title: "Shapefile drawing using Python"
date: 2016-03-08
---

Last week, I needed to draw some maps and display data on these maps also. I have spent some hours to discover how to complete this task. Thus, in this post, I will summarize step by step to accomplish the initial goal.

**Basic drawing**

1. First time first, we need to download the shapefile before doing anything. Luckily, [**Open street map**](https://osm.wno-edv-service.de/boundaries/) is an open source data for us to download the shapefile of boundary of many countries. However, do not forget to register an account to download. The data is quite complete and ready to use. I also put the [demo data of Singapore](/assets/Singapore_AL2.shp), and it is used to illustrate latter steps.
2. Secondly, we need to choose the library to draw. [BaseMap](http://matplotlib.org/basemap/) is a common lib for drawing shapefile but it is overkilled in my situation i.e. I do not need to use its fancy features. Thus, [pyshp](https://pypi.python.org/pypi/pyshp) is my selection. It is lightweight but still powerful enough to satisfy my requirement. Moreover, installation and usage are as easy as ABC :-) . Last but not least, I have used Python 2.7 and matplotlib 1.4.2 to draw but the conversion to Python 3.x is not hard.
3. Let us draw :-D

```python
# import libraries
import shapefile as shp
import matplotlib.pyplot as plt

#load shapefile
sf = shp.Reader('Singapore_AL2.shp')

plt.figure()
for shape in sf.shapeRecords():
    
    # end index of each components of map
    l = shape.shape.parts
    
    len_l = len(l)  # how many parts of countries i.e. land and islands
    x = [i[0] for i in shape.shape.points[:]] # list of latitude
    y = [i[1] for i in shape.shape.points[:]] # list of longitude
    l.append(len(x)) # ensure the closure of the last component
    for k in xrange(len_l):
        # draw each component of map.
        # l[k] to l[k + 1] is the range of points that make this component
        plt.plot(x[l[k]:l[k + 1]],y[l[k]:l[k + 1]], 'k-')

# display
plt.show()
```

The final result is not bad.
<img src="/assets/2016_03_08/plain_Singapore.png">
