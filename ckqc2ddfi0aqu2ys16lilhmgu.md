# 15- Compute new field values of attribute table

Create vector layer

```
vl = QgsVectorLayer("Point", "Cities_Kurdistan", "memory")

from qgis.PyQt.QtCore import QVariant
pr = vl.dataProvider()
```
Add an attributed table to it

```
pr.addAttributes([QgsField("City", QVariant.String),
                  QgsField("Population",  QVariant.Double),
                  QgsField("Area", QVariant.Double),
                  QgsField("Density", QVariant.Double)])
vl.updateFields()

QgsProject.instance().addMapLayer(vl)
```
Define data

```
my_data = [
    {'x': 44.01, 'y': 36.19, 'City': 'Erbil', 'Population': 2932800, 'Area': 14872},
    {'x': 45.43, 'y': 35.55, 'City': 'Sulaymania', 'Population': 1967000, 'Area': 20143},
    {'x': 42.99, 'y': 36.86, 'City': 'Duhok', 'Population': 1292535, 'Area': 10955},
    {'x': 45.98, 'y': 35.17, 'City': 'Halabja', 'Population': 109000, 'Area': 889}]
```
Add data to the fields

```
for rec in my_data:
    f = QgsFeature()
    pt = QgsPointXY(rec['x'], rec['y'])
    f.setGeometry(QgsGeometry.fromPointXY(pt))
    f.setAttributes([rec['City'], rec['Population'], rec['Area']])
    pr.addFeature(f)
 
vl.updateExtents() 
QgsProject.instance().addMapLayer(vl)
```
The density field is empty and we compute it with for loop

```
with edit(vl):
    for f in vl.getFeatures():
        f['Density'] = f['Population'] / f['Area']
        vl.updateFeature(f)
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>