---
title: "13- Chaining PyQGIS Processes: A Step-by-Step Guide with Real-World Data from Erbil, Iraq."
datePublished: Fri Jun 25 2021 08:17:33 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2a8bk0avb48s124iaav0w
slug: 13-chaining-pyqgis-processes-a-step-by-step-guide-with-real-world-data-from-erbil-iraq
tags: programming-blogs, python, learning, gis

---

Looking to enhance your skills in PyQGIS? Look no further! This article provides a step-by-step guide on how to chain processes in PyQGIS using real-world data from the city of Erbil in Iraq. Follow along as we show you how to select primary roads, create buffers, find places along those roads, and print their names. By the end of this tutorial, you'll have a solid understanding of how to chain processes in PyQGIS and be able to apply this knowledge to your own projects.

To begin, download the [**data**](https://github.com/Azad77/Python_qgis/blob/main/Data/places%26roads.zip) we'll be using in this tutorial. We'll start by loading shapefiles of roads and places from the city of Erbil in Iraq:

```python
roa = "D:/erbil_data/erbil_data/roads.shp"
pla = "D:/erbil_data/erbil_data/places.shp"
```

Next, we'll choose only the primary roads from the roads shapefile:

```python
expression = "fclass = 'primary'"

primary_roads = processing.run("native:extractbyexpression",
	{"INPUT":roa, "EXPRESSION":expression,"OUTPUT":"memory:"}
	)["OUTPUT"]
```

Then, we'll create a buffer around the primary roads:

```python
buffered_primary_roads = processing.run("native:buffer",
    {'INPUT':primary_roads,'DISTANCE':0.01,'SEGMENTS':5,'END_CAP_STYLE':0,
    'JOIN_STYLE':0,'MITER_LIMIT':2,'DISSOLVE':False,'OUTPUT':'memory:'}
    )['OUTPUT']
```

We can then add the layer of buffered primary roads:

```python
QgsProject.instance().addMapLayer(buffered_primary_roads)
```

Next, we'll find the places along the primary roads:

```python
places_along_primary_roads = processing.run("native:extractbylocation",
	{"INPUT": pla, "PREDICATE": [0], "INTERSECT":buffered_primary_roads, "OUTPUT": "memory:"}
	)['OUTPUT']
```

And we'll add the layer of places along the primary roads:

```python
QgsProject.instance().addMapLayer(places_along_primary_roads)
```

Finally, we'll print the name of each place along the primary roads:

```python
for feature in places_along_primary_roads.getFeatures():
    print(feature["name"])
```

In conclusion, this article provides a detailed tutorial on how to chain processes in PyQGIS using real-world data from the city of Erbil in Iraq. By following the step-by-step guide, readers can learn how to select primary roads, create buffers, find places along those roads, and print their names. This knowledge can then be applied to their own PyQGIS projects.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content