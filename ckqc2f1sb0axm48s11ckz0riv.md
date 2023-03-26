---
title: "16- Streamlining GeoPackage Layer Loading in PyQGIS with Custom Functions"
datePublished: Fri Jun 25 2021 08:21:18 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2f1sb0axm48s11ckz0riv
slug: 16-streamlining-geopackage-layer-loading-in-pyqgis-with-custom-functions
tags: programming-blogs, python, learning, gis

---

The article explains how to streamline GeoPackage layer loading in PyQGIS with custom functions. It provides examples of functions to add new layers, multiple layers, and all layers. It also includes a link to download sample data.

To get started, we need to download sample data in the GeoPackage format. The article provides a [link](https://github.com/Azad77/Python_qgis/blob/main/Data/osopentoid_202105_gpkg_sr.zip) to download a GeoPackage file containing sample data. Once downloaded, we can unzip the file and load it into PyQGIS.

First, loading a list of layer names in the GeoPackage:

```python
from osgeo import ogr
gpkg1 = 'D:/Python_QGIS/data/osopentoid_202105_gpkg_sr/osopentoid_202105_sr.gpkg'
gpkg_layers = [n.GetName() for n in ogr.Open(gpkg1)]
print(gpkg_layers)
print('os_mastermap_topography_layer' in gpkg_layers)
# True
print('london_boroughs' in gpkg_layers)
# False (because the layer is not available)
```

Writing a function to add new layers:

```python
def add_layer(gpkg, layer):
    layers = [n.GetName() for n in ogr.Open(gpkg)]
    if layer in layers:
        iface.addVectorLayer(gpkg + "|layername=" + layer, layer, 'ogr')
    else:
        print('Error: there is no layer named "{}" in {}!'.format(layer, gpkg))
```

Use the defined add\_layer function to add a new layer:

```python
add_layer(gpkg1, 'os_mastermap_topography_layer')
```

Function to add multiple layers:

```python
def add_layers(gpkg, layers):
    for layer in layers:
        add_layer(gpkg, layer)

add_layers(gpkg1, ['os_mastermap_sites_layer', 'os_mastermap_highways_network'])
```

A function to add all layers:

```python
def add_all_layers(gpkg):
    layers = [n.GetName() for n in ogr.Open(gpkg)]
    add_layers(gpkg, layers)
    
add_all_layers(gpkg1)
```

In conclusion, the article provides useful insights into how to streamline GeoPackage layer loading in PyQGIS with custom functions. It offers examples of functions to add new layers, multiple layers, and all layers. The article also includes a link to download sample data, which readers can use to practice the concepts discussed. Overall, this article is a valuable resource for anyone looking to improve their GeoPackage layer loading process in PyQGIS.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content