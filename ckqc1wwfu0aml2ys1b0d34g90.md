---
title: "6- Retrieving information of vector layer"
datePublished: Fri Jun 25 2021 08:07:11 GMT+0000 (Coordinated Universal Time)
cuid: ckqc1wwfu0aml2ys1b0d34g90
slug: 6-retrieving-information-of-vector-layer-1
tags: programming-blogs, python, learning, basics, gis

---

Learn how to retrieve information about the fields of a vector layer in QGIS with the help of the *fields()* function. In this article, we'll explore how to use this function on a *QgsVectorLayer* to extract useful information about the fields of a vector layer. Whether you're a GIS professional or a beginner, this guide will help you better understand how to work with vector layers in QGIS.

```plaintext
uri = "D:/Python_QGIS/data/Countries.shp"
vlayer = QgsVectorLayer(uri, "Countries", "ogr")

for field in vlayer.fields():
        print(field.name())
```

In conclusion, this article provides a helpful guide on how to retrieve information about the fields of a vector layer in QGIS using the *fields()* function. The article is suitable for both GIS professionals and beginners who are looking to better understand how to work with vector layers in QGIS. By following the steps outlined in the article, users can easily extract useful information about the fields of a vector layer in QGIS.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content