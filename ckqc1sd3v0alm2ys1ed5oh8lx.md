---
title: "4- Loading Vector Layers with PyQGIS: A Step-by-Step Guide"
datePublished: Fri Jun 25 2021 08:03:39 GMT+0000 (Coordinated Universal Time)
cuid: ckqc1sd3v0alm2ys1ed5oh8lx
slug: 4-loading-vector-layers-with-pyqgis-a-step-by-step-guide
tags: programming-blogs, python, learning, basics, gis

---

Are you searching for a step-by-step guide on how to load vector layers using QGIS? Look no further! In this article, we will guide you through the process of downloading the required data and retrieving the path of the shapefile. With our easy-to-follow instructions, you will be able to add vector layers to your QGIS project in no time.

You can download the data we are using from this [**link**](https://github.com/Azad77/Python_qgis/blob/main/Data/Countries.zip).

Then, retrieve the path of the shapefile using the following code:

```plaintext
uri = "D:/Python_QGIS/data/Countries.shp"
```

The format of the code is:

```plaintext
vlayer = iface.addVectorLayer(data_source, layer_name, provider_name)
```

To load our shapefile, use the following code:

```plaintext
iface.addVectorLayer(uri, "countries", "ogr")
```

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content