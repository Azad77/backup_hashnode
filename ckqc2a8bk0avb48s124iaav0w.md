# 13- Chaining Processings

Download the  [data](https://github.com/Azad77/Python_qgis/blob/main/Data/places%26roads.zip) 

Loading shapefiles of roads and some places of Erbil city in Iraq
```
roa = "D:/erbil_data/erbil_data/roads.shp"
pla = "D:/erbil_data/erbil_data/places.shp"
```
Choose only primary roads from the roads shapefile

```
expression = "fclass = 'primary'"

primary_roads = processing.run("native:extractbyexpression",
	{"INPUT":roa, "EXPRESSION":expression,"OUTPUT":"memory:"}
	)["OUTPUT"]
```

Create a buffer around primary roads

```
buffered_primary_roads = processing.run("native:buffer",
    {'INPUT':primary_roads,'DISTANCE':0.01,'SEGMENTS':5,'END_CAP_STYLE':0,
    'JOIN_STYLE':0,'MITER_LIMIT':2,'DISSOLVE':False,'OUTPUT':'memory:'}
    )['OUTPUT']
```
Add the layer of buffered_primary_roads

```
QgsProject.instance().addMapLayer(buffered_primary_roads)
```
Find places along primary rods

```
places_along_primary_roads = processing.run("native:extractbylocation",
	{"INPUT": pla, "PREDICATE": [0], "INTERSECT":buffered_primary_roads, "OUTPUT": "memory:"}
	)['OUTPUT']
QgsProject.instance().addMapLayer(places_along_primary_roads)
```

Print the name of places along primary roads

```
for feature in places_along_primary_roads.getFeatures():
    print(feature["name"])
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>