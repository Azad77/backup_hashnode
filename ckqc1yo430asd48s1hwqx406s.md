---
title: "7- Show the attribute table of a vector layer"
datePublished: Fri Jun 25 2021 08:08:33 GMT+0000 (Coordinated Universal Time)
cuid: ckqc1yo430asd48s1hwqx406s
slug: 7-show-the-attribute-table-of-a-vector-layer
tags: programming-blogs, python, learning, gis

---

As a GIS enthusiast, you know that one of the most important aspects of working with vector layers is the ability to view and manipulate attribute data. Fortunately, QGIS provides a simple way to access this information with the *iface.showAttributeTable()* function. In this article, we'll explore how to use this function to open the attribute table of a vector layer, so you can quickly access and analyze the data you need.

```plaintext
uri = "D:/Python_QGIS/data/Countries.shp"
vlayer = QgsVectorLayer(uri, "Countries", "ogr")

iface.showAttributeTable(vlayer)
```

QGIS provides a simple way to access attribute data with the *iface.showAttributeTable()* function. This function enables users to open the attribute table of a vector layer, which is essential for viewing and manipulating attribute data. By using this function, GIS enthusiasts can quickly access and analyze the data they need. Overall, the ability to view and manipulate attribute data is crucial in GIS, and QGIS provides an efficient way to do so.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content