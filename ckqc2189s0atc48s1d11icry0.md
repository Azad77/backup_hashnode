# 8- Iterating over a layer

Load a raster layer:

```
uri = "D:/Python_QGIS/data/dem_subset.tif"
rlayer = iface.addRasterLayer(uri, "my_raster", "gdal")
``` 

Check if the raster layer is valid or not:
```
if rlayer.isValid():
    print("Great this is a valid raster layer!")
else: 
    print("This is invalid raster layer!")
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote> 