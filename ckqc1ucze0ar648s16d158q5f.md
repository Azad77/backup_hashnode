---
title: "5- Loading raster files"
datePublished: Fri Jun 25 2021 08:05:12 GMT+0000 (Coordinated Universal Time)
cuid: ckqc1ucze0ar648s16d158q5f
slug: 5-loading-raster-files-1
tags: programming-blogs, python, learning, gis

---

To load raster files in QGIS, the GDAL library is commonly used. In order to follow along with the examples in this tutorial, you will need to first download the data we will be working with from the following link: [**data**](https://github.com/Azad77/Python_qgis/blob/main/Data/dem_subset.tif).

Next, you will need to get the path of the downloaded raster file. For example:

```plaintext
plaintextCopy codeuri = "D:/Python_QGIS/data/dem_subset.tif"
```

With the path to the raster file, you can now add the layer to QGIS using the following format:

```
plaintextCopy coderlayer = iface.addRasterLayer(data_source, layer_name, provider_name)
```

To load the raster file into QGIS using PyQGIS, use the following code in the Python console:

```plaintext
plaintextCopy coderlayer = iface.addRasterLayer(uri, "my_raster", "gdal")
```

In summary, this article explains how to use PyQGIS to load raster files into QGIS using the GDAL library. It provides step-by-step instructions on how to add a layer to QGIS, and includes a link to download the data used in the example code.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content