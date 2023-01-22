# 4- Loading a vector layer

You can download the  [data](https://github.com/Azad77/Python_qgis/blob/main/Data/Countries.zip)  that we are using.


<p>Then, get the path of the shapefile</p>

```
uri = "D:/Python_QGIS/data/Countries.shp" 
``` 


The format is:
<p>vlayer = iface.addVectorLayer(data_source, layer_name, provider_name)</p>

```
iface.addVectorLayer(uri, "countries", "ogr")
```