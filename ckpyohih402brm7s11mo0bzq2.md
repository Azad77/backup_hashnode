# 7- Show attribute table of a vector layer

We can use *iface.showAttributeTable()* function for opening attribute table of a vector layer:

```
uri = "D:/Python_QGIS/data/Countries.shp"
vlayer = QgsVectorLayer(uri, "Countries", "ogr")

iface.showAttributeTable(vlayer)
``` 