# 6- Retrieving information of vector layer

We use *fields()* on a *QgsVectorLayer* to retrieve information about the fields of a vector layer.


```
uri = "D:/Python_QGIS/data/Countries.shp"
vlayer = QgsVectorLayer(uri, "Countries", "ogr")

for field in vlayer.fields():
        print(field.name())
``` 

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>