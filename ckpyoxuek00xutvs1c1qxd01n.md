# 14- Managing Project Layers

```
import processing
uri = "D:/Python_QGIS/data/places.shp"
vlayer = iface.addVectorLayer(uri, "Places", "ogr")
```
Useing *runAndLoadResults()* function to create buffer

```
processing.runAndLoadResults("native:buffer", {'INPUT':uri,'DISTANCE':0.1,'SEGMENTS':5,'END_CAP_STYLE':0,'JOIN_STYLE':0,'MITER_LIMIT':2,'DISSOLVE':False,'OUTPUT':'memory:'})

project = QgsProject.instance()
print(project.mapLayers())
```
It returns: 
{'output_1a4a410f_b372_49ca_87d4_e6aeba988509': <qgis._core.QgsVectorLayer object at 0x000001CCDAE1A3A8>, 'places_a7c9b8cb_2aee_47e0_8101_5caf81e9607c': <qgis._core.QgsVectorLayer object at 0x000001CCDAE1A288>}

<p> Print name of layers with for loop</p>
```
for id, layer in project.mapLayers().items():
    print(layer.name())
 ```

Rename a layer 
```
rename = project.mapLayersByName('Buffered')[0]
rename.setName('Renamed!')
```

Remove a layer
```
delete = project.mapLayersByName('Places')[0]
project.removeMapLayer(delete.id())
```