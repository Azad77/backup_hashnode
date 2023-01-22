# 20- Calculating distance between two points

```
from qgis.core import QgsDistanceArea

d = QgsDistanceArea()
d.setEllipsoid('WGS84')


Erbil = QgsPointXY(44.01, 36.19)
Duhok = QgsPointXY(42.99, 36.86)

distance = d.measureLine([Erbil, Duhok])
print(distance/1000)
```