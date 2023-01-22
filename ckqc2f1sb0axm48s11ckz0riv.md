# 16- Load GeoPackage layers by function

Download a gpgk  [data](https://github.com/Azad77/Python_qgis/blob/main/Data/osopentoid_202105_gpkg_sr.zip),  then unzip it.

Loading a list of layer names in the GeoPackage:

```
from osgeo import ogr
gpkg1 = 'D:/Python_QGIS/data/osopentoid_202105_gpkg_sr/osopentoid_202105_sr.gpkg'
gpkg_layers = [n.GetName() for n in ogr.Open(gpkg1)]
print(gpkg_layers)
print('os_mastermap_topography_layer' in gpkg_layers)

print('london_boroughs' in gpkg_layers)
```
Python Console returns "False" because the layer not available


Writing a function to add new layers:
```
def add_layer(gpkg, layer):
    layers = [n.GetName() for n in ogr.Open(gpkg)]
    if layer in layers:
        iface.addVectorLayer(gpkg + "|layername=" + layer, layer, 'ogr')
    else:
        print('Error: there is no layer named "{}" in {}!'.format(layer, gpkg))
```            
Use defined add_layer function to add a new layer
```
add_layer(gpkg1, 'os_mastermap_topography_layer')
```

Function to add multiple layers:
```
def add_layers(gpkg, layers):
    for layer in layers:
        add_layer(gpkg, layer)

add_layers(gpkg1, ['os_mastermap_sites_layer', 'os_mastermap_highways_network'])
```
A function to add all layers:
```
def add_all_layers(gpkg):
    layers = [n.GetName() for n in ogr.Open(gpkg)]
    add_layers(gpkg, layers)
    
add_all_layers(gpkg1)
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>