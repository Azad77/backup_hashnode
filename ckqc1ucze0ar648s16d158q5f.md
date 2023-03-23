---
title: "5- Loading raster files"
datePublished: Fri Jun 25 2021 08:05:12 GMT+0000 (Coordinated Universal Time)
cuid: ckqc1ucze0ar648s16d158q5f
slug: 5-loading-raster-files-1
tags: programming-blogs, python, learning, gis

---

For loading raster files, GDAL library is used in QGIS.

Firstly, download the [data](https://github.com/Azad77/Python_qgis/blob/main/Data/dem_subset.tif) we are using.

Then, get the path of the raster file:

```plaintext
uri = "D:/Python_QGIS/data/dem_subset.tif"
```

Now add the layer

The format of the code is:

```plaintext
rlayer = iface.addRasterLayer(data_source, layer_name, provider_name)
```

Now, let's load the raster file into QGIS using PyQGIS. In the Python console, use the following code:

```plaintext
rlayer = iface.addRasterLayer(uri, "my_raster", "gdal")
```

In conclusion, the GDAL library is used in QGIS for loading raster files. The article provides steps on how to load a raster file using PyQGIS and the format of the code needed to add the layer. The article also provides a link to download the data used in the example code.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content