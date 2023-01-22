# 9- Create a vector layer and add fields to it

Firstly, create a new *QgsVectorLayer*
```
vl = QgsVectorLayer("Point", "shapefile", "memory")
```

Add attribute table

```
from qgis.PyQt.QtCore import QVariant
pr = vl.dataProvider()
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Int),
                  QgsField("Area", QVariant.Double)])
```

Use *updateFields()* to fetch changes from the provider

```
vl.updateFields()

fet = QgsFeature()
fet.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(44.01,36.19)))
fet.setAttributes(["Erbil", 2000000, 300])
pr.addFeature(fet)
```
After new features have been added, we update layer's extent
```
vl.updateExtents()
QgsProject.instance().addMapLayer(vl)
``` 

### Add a list of items to the fields

 
```
vl = QgsVectorLayer("Point", "Cities_Kurdistan", "memory")

from qgis.PyQt.QtCore import QVariant
pr = vl.dataProvider()
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Double),
                  QgsField("Area", QVariant.Double)])
vl.updateFields()

QgsProject.instance().addMapLayer(vl)
```
Add a list of items:

```
f1 = QgsFeature()
f1.setAttributes(['Erbil', '2932800', '14872'])
f1.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(44.01,36.19)))

f2 = QgsFeature()
f2.setAttributes(['Sulaymania', '1967000', '20143'])
f2.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(45.43,35.55)))

f3 = QgsFeature()
f3.setAttributes(['Duhok', '1292535', '10955'])
f3.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(42.99,36.86)))

f4 = QgsFeature()
f4.setAttributes(['Halabja', '109000', '889'])
f4.setGeometry(QgsGeometry.fromPointXY(QgsPointXY(45.98,35.17)))

vl.dataProvider().addFeatures([f1, f2, f3, f4])

vl.updateExtents()
``` 