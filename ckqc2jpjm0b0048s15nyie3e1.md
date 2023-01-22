# 19- Delete a column of vector layer attribute

Firstly, open a shapefile that has an attribute table.

To delete the third column of the table use this code:

```
layer = iface.activeLayer()
layer.startEditing()
layer.deleteAttribute(2)
layer.commitChanges()
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>