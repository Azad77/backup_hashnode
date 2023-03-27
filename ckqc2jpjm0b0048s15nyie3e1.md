---
title: "19- How to Delete a Column from a Vector Layer Attribute in PyQGIS"
datePublished: Fri Jun 25 2021 08:24:55 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2jpjm0b0048s15nyie3e1
slug: 19-how-to-delete-a-column-from-a-vector-layer-attribute-in-pyqgis
tags: tutorial, programming-blogs, python, learning, gis

---

Learn how to delete a column from a vector layer attribute in PyQGIS by following these simple steps. This tutorial will guide you through the process of opening a shapefile with an attribute table and using a code snippet to remove a specific column from the table. Whether you're a beginner or an experienced user, this guide will help you streamline your workflow and improve your data management skills in PyQGIS.

To begin, open a shapefile that has an attribute table. To delete the third column of the table, use the following code snippet:

```python
# Get the currently active layer:
layer = iface.activeLayer()

# Begin editing the layer:
layer.startEditing()

# Delete the attribute with the index of 2 from the layer:
layer.deleteAttribute(2)

# Commit the changes made to the layer
layer.commitChanges()
```

In conclusion, deleting a column from a vector layer attribute in PyQGIS is a simple process that can be accomplished by following the steps outlined in this tutorial. With the help of the code snippet provided, users can easily remove a specific column from their attribute table and streamline their workflow in PyQGIS.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content