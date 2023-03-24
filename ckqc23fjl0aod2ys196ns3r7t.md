---
title: "9- Creating Vector Layers and Adding Fields in PyQGIS: A Step-by-Step Guide"
datePublished: Fri Jun 25 2021 08:12:15 GMT+0000 (Coordinated Universal Time)
cuid: ckqc23fjl0aod2ys196ns3r7t
slug: 9-creating-vector-layers-and-adding-fields-in-pyqgis-a-step-by-step-guide
tags: programming-blogs, python, learning, gis

---

Are you looking to create vector layers and add fields in PyQGIS? Look no further! In this step-by-step guide, we will walk you through the process of creating a new QgsVectorLayer, adding an attribute table, updating fields, and adding new features to your layer. We will also cover how to update the layer's extent and add a list of items to your fields. Whether you're a seasoned PyQGIS user or just starting out, this guide is perfect for anyone looking to enhance their skills and take their geospatial data analysis to the next level. So, let's dive in!

Firstly, create a new QgsVectorLayer*:*

```plaintext
vl = QgsVectorLayer("Point", "shapefile", "memory")
```

Add an attribute table:

```python
from qgis.PyQt.QtCore import QVariant
pr = vl.dataProvider()
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Int),
                  QgsField("Area", QVariant.Double)])
vl.updateFields()
```

Add new features to the layer:

```python
fet = QgsFeature()
fet.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(44.01,36.19)))
fet.setAttributes(["Erbil", 2000000, 300])
pr.addFeatures([fet])
vl.updateExtents()
```

Add the layer to the project:

```python
QgsProject.instance().addMapLayer(vl)
```

Create a new QgsVectorLayer and add an attribute table:

```python
vl = QgsVectorLayer("Point", "Cities_Kurdistan", "memory")
pr = vl.dataProvider()
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Double),
                  QgsField("Area", QVariant.Double)])
vl.updateFields()
```

Add new features to the layer:

```python
f1 = QgsFeature()
f1.setAttributes(['Erbil', 2932800.0, 14872.0])
f1.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(44.01,36.19)))

f2 = QgsFeature()
f2.setAttributes(['Sulaymania', 1967000.0, 20143.0])
f2.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(45.43,35.55)))

f3 = QgsFeature()
f3.setAttributes(['Duhok', 1292535.0, 10955.0])
f3.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(42.99,36.86)))

f4 = QgsFeature()
f4.setAttributes(['Halabja', 109000.0, 889.0])
f4.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(45.98,35.17)))

pr.addFeatures([f1, f2, f3, f4])
vl.updateExtents()
```

Add the layer to the project:

```python
QgsProject.instance().addMapLayer(vl)
```

The overall code is:

```python
# Create a new QgsVectorLayer
vl = QgsVectorLayer("Point", "shapefile", "memory")

# Add an attribute table
from qgis.PyQt.QtCore import QVariant
pr = vl.dataProvider()
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Int),
                  QgsField("Area", QVariant.Double)])
vl.updateFields()

# Add new features to the layer
fet = QgsFeature()
fet.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(44.01,36.19)))
fet.setAttributes(["Erbil", 2000000, 300])
pr.addFeatures([fet])
vl.updateExtents()

# Add the layer to the project
QgsProject.instance().addMapLayer(vl)

# Create a new QgsVectorLayer and add an attribute table
vl = QgsVectorLayer("Point", "Cities_Kurdistan", "memory")
pr = vl.dataProvider()
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Double),
                  QgsField("Area", QVariant.Double)])
vl.updateFields()

# Add new features to the layer
f1 = QgsFeature()
f1.setAttributes(['Erbil', 2932800.0, 14872.0])
f1.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(44.01,36.19)))

f2 = QgsFeature()
f2.setAttributes(['Sulaymania', 1967000.0, 20143.0])
f2.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(45.43,35.55)))

f3 = QgsFeature()
f3.setAttributes(['Duhok', 1292535.0, 10955.0])
f3.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(42.99,36.86)))

f4 = QgsFeature()
f4.setAttributes(['Halabja', 109000.0, 889.0])
f4.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(45.98,35.17)))

pr.addFeatures([f1, f2, f3, f4])
vl.updateExtents()

# Add the layer to the project
QgsProject.instance().addMapLayer(vl)
```

In conclusion, this step-by-step guide provides a comprehensive overview of creating vector layers and adding fields in PyQGIS. The guide covers essential topics such as creating a new QgsVectorLayer, adding an attribute table, updating fields, and adding new features to your layer. Additionally, the guide also covers how to update the layer's extent and add a list of items to your fields. Whether you're an experienced PyQGIS user or just starting, this guide is an excellent resource to enhance your skills and take your geospatial data analysis to the next level.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content