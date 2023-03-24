---
title: "11- Execute QGIS processing algorithms using Python"
datePublished: Fri Jun 25 2021 08:15:00 GMT+0000 (Coordinated Universal Time)
cuid: ckqc26yqj0ap12ys13pr27cmn
slug: 11-execute-qgis-processing-algorithms-using-python
tags: programming-blogs, python, learning, basics, gis

---

Are you looking for a way to execute QGIS processing algorithms using Python? Look no further than the [`processing.run`](http://processing.run) method in PyQGIS! With just two arguments - the name of the algorithm and a dictionary of algorithm parameters - you can easily create buffers and load them as new layers.

[`processing.run`](http://processing.run) is a method in PyQGIS that allows you to execute QGIS processing algorithms using Python. The method takes two arguments: the name of the algorithm as a string and a dictionary of algorithm parameters.

Identify the path of the shapefile:

```python
uri = "D:/Python_QGIS/data/KRG_Cities.shp"
```

Using the processing.*run() method to create a buffer to the shapefile:*

```python
processing.run("native:buffer", {'INPUT': uri,
               'DISTANCE': 100.0,
               'SEGMENTS': 10,
               'DISSOLVE': True,
               'END_CAP_STYLE': 0,
               'JOIN_STYLE': 0,
               'MITER_LIMIT': 10,
               'OUTPUT': 'D:/Python_QGIS/data/buffers.shp'})
```

Load the result as a new layer using the "processing.runAndLoadResults" method*:*

```python
processing.runAndLoadResults("native:buffer", 
                {'INPUT':uri,
                'DISTANCE':1,
                'SEGMENTS':5,
                'END_CAP_STYLE':0,
                'JOIN_STYLE':0,
                'MITER_LIMIT':2,
                'DISSOLVE':False,
                'OUTPUT':'memory:'})
```

In conclusion, the article explains how to execute QGIS processing algorithms using Python with the help of the [`processing.run`](http://processing.run) method in PyQGIS. By providing the name of the algorithm and a dictionary of algorithm parameters, users can create buffers and load them as new layers. The article also provides an example of how to identify the path of a shapefile, create a buffer to it, and load the result as a new layer using the `processing.runAndLoadResults` method.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content