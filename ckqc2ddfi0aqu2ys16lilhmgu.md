---
title: "15- Effortlessly Compute New Field Values in PyQGIS with this Step-by-Step Tutorial"
datePublished: Fri Jun 25 2021 08:19:59 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2ddfi0aqu2ys16lilhmgu
slug: 15-effortlessly-compute-new-field-values-in-pyqgis-with-this-step-by-step-tutorial
tags: programming-blogs, python, learning, gis

---

If you are struggling with computing new field values in PyQGIS, this step-by-step tutorial is the perfect resource for you. In this tutorial, we will guide you through the process of creating a vector layer, adding an attributed table to it, adding data to its fields, and computing new field values using a for loop. Specifically, we will show you how to compute the density field. Whether you are a beginner or an experienced PyQGIS user, you will find this tutorial helpful in enhancing your skills and improving your data analysis capabilities.

By following the instructions in this tutorial, you will be able to create a vector layer, add data to its fields, and compute new field values using a for loop. We have provided a complete code for your reference. The tutorial is suitable for both beginners and experienced PyQGIS users. Key takeaways from this tutorial include the ability to:

* Create a vector layer with an attributed table
    
* Add data to the fields of the vector layer
    
* Compute new field values using a for loop
    

First, create a vector layer:

```python
from qgis.PyQt.QtCore import QVariant
from qgis.core import edit

vl = QgsVectorLayer("Point", "Cities_Kurdistan", "memory")

pr = vl.dataProvider()
```

Next, add an attributed table to it:

```python
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Double),
                  QgsField("Area", QVariant.Double),
                  QgsField("Density", QVariant.Double)])
vl.updateFields()
```

Then, define your data:

```python
my_data = [
    {'x': 44.01, 'y': 36.19, 'City': 'Erbil', 'Population': 2932800, 'Area': 14872},
    {'x': 45.43, 'y': 35.55, 'City': 'Sulaymania', 'Population': 1967000, 'Area': 20143},
    {'x': 42.99, 'y': 36.86, 'City': 'Duhok', 'Population': 1292535, 'Area': 10955},
    {'x': 45.98, 'y': 35.17, 'City': 'Halabja', 'Population': 109000, 'Area': 889}]
```

After that, add data to the fields:

```python
for rec in my_data:
    f = QgsFeature()
    pt = QgsPointXY(rec['x'], rec['y'])
    f.setGeometry(QgsGeometry.fromPointXY(pt))
    f.setAttributes([rec['City'], rec['Population'], rec['Area']])
    pr.addFeature(f)
 
vl.updateExtents() 
QgsProject.instance().addMapLayer(vl)
```

The **density** field is currently empty, and we will compute it with a for loop:

```python
with edit(vl):
    for f in vl.getFeatures():
        f['Density'] = f['Population'] / f['Area']
        vl.updateFeature(f)
```

The complete code is:

```python
from qgis.PyQt.QtCore import QVariant
from qgis.core import edit

vl = QgsVectorLayer("Point", "Cities_Kurdistan", "memory")
pr = vl.dataProvider()

# add attributes
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Double),
                  QgsField("Area", QVariant.Double),
                  QgsField("Density", QVariant.Double)])
vl.updateFields()

#define your data
my_data = [
    {'x': 44.01, 'y': 36.19, 'City': 'Erbil', 'Population': 2932800, 'Area': 14872},
    {'x': 45.43, 'y': 35.55, 'City': 'Sulaymania', 'Population': 1967000, 'Area': 20143},
    {'x': 42.99, 'y': 36.86, 'City': 'Duhok', 'Population': 1292535, 'Area': 10955},
    {'x': 45.98, 'y': 35.17, 'City': 'Halabja', 'Population': 109000, 'Area': 889}]

# add data to the fields    
for rec in my_data:
    f = QgsFeature()
    pt = QgsPointXY(rec['x'], rec['y'])
    f.setGeometry(QgsGeometry.fromPointXY(pt))
    f.setAttributes([rec['City'], rec['Population'], rec['Area']])
    pr.addFeature(f)
 
vl.updateExtents() 
QgsProject.instance().addMapLayer(vl)

# compute "Density":
with edit(vl):
    for f in vl.getFeatures():
        f['Density'] = f['Population'] / f['Area']
        vl.updateFeature(f)
```

In conclusion, this tutorial provides a comprehensive guide to computing new field values in PyQGIS. We hope that you find this tutorial helpful in enhancing your skills and improving your data analysis capabilities.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content