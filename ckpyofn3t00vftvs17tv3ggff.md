# 6- Retrieving information of vector layer

We use *fields()* on a *QgsVectorLayer* to retrieve information about the fields of a vector layer.


```
uri = "D:/Python_QGIS/data/Countries.shp"
vlayer = QgsVectorLayer(uri, "Countries", "ogr")

for field in vlayer.fields():
        print(field.name())
``` 