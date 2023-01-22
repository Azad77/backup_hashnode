# 19- Delete a column of vector layer attribute

Firstly, open a shapefile that has an attribute table.

To delete the third column of the table use this code:

```
layer = iface.activeLayer()
layer.startEditing()
layer.deleteAttribute(2)
layer.commitChanges()
```