---
title: "20- How to Calculate the Distance Between Two Points in PyQGIS"
datePublished: Fri Jun 25 2021 08:26:13 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2ldnm0b0r48s17sacd3bp
slug: 20-how-to-calculate-the-distance-between-two-points-in-pyqgis
tags: tutorial, programming-blogs, python, learning, gis

---

```python
# import the necessary module
from qgis.core import QgsDistanceArea

# create a new QgsDistanceArea instance
d = QgsDistanceArea()

# set the ellipsoid to use for the measurement (in this case, WGS84)
d.setEllipsoid('WGS84')

# create two QgsPointXY instances representing the coordinates of Erbil and Duhok
Erbil = QgsPointXY(44.01, 36.19)
Duhok = QgsPointXY(42.99, 36.86)

# calculate the distance between the two points using the QgsDistanceArea instance
distance = d.measureLine([Erbil, Duhok])

# print the result of the distance calculation, converted from meters to kilometers
print("The distance between Erbil and Huhok is", distance / 1000, "KM")
```

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content