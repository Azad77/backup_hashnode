# 7- Show attribute table of a vector layer

We can use *iface.showAttributeTable()* function for opening attribute table of a vector layer:

```
uri = "D:/Python_QGIS/data/Countries.shp"
vlayer = QgsVectorLayer(uri, "Countries", "ogr")

iface.showAttributeTable(vlayer)
``` 

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>