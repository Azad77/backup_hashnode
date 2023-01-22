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