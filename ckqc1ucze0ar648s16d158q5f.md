# 5- Loading raster files

For loading raster files, GDAL library is used.

Firstly, download the  [data](https://github.com/Azad77/Python_qgis/blob/main/Data/dem_subset.tif).

Then, get the path of the raster file:

```
uri = "D:/Python_QGIS/data/dem_subset.tif"
```

Now add the layer

The format is:

<p>rlayer = iface.addRasterLayer(data_source, layer_name, provider_name)</p>

```
rlayer = iface.addRasterLayer(uri, "my_raster", "gdal")
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>