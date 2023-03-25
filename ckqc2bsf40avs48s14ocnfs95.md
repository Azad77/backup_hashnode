---
title: "14- Managing Project Layers"
datePublished: Fri Jun 25 2021 08:18:45 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2bsf40avs48s14ocnfs95
slug: 14-managing-project-layers-1
tags: programming-blogs, python, learning, gis

---

```python
import processing
uri = "D:/Python_QGIS/data/places.shp"
vlayer = iface.addVectorLayer(uri, "Places", "ogr")
```

Useing *runAndLoadResults()* function to create buffer

```python
processing.runAndLoadResults("native:buffer", {'INPUT':uri,'DISTANCE':0.1,'SEGMENTS':5,'END_CAP_STYLE':0,'JOIN_STYLE':0,'MITER_LIMIT':2,'DISSOLVE':False,'OUTPUT':'memory:'})

project = QgsProject.instance()
print(project.mapLayers())
```

Rename a layer

```python
rename = project.mapLayersByName('Buffered')[0]
rename.setName('Renamed!')
```

Remove a layer

```python
delete = project.mapLayersByName('Places')[0]
project.removeMapLayer(delete.id())
```

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content