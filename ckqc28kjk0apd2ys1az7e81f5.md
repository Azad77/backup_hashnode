---
title: "12- Map Printing Made Easy with PyQGIS"
datePublished: Fri Jun 25 2021 08:16:15 GMT+0000 (Coordinated Universal Time)
cuid: ckqc28kjk0apd2ys1az7e81f5
slug: 12-map-printing-made-easy-with-pyqgis
tags: programming-blogs, python, learning, gis

---

![Layout.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623514088236/0S5bBpoF3.png align="left")

Learn how to easily print maps using PyQGIS with this step-by-step guide. PyQGIS is a Python library that provides access to QGIS API, allowing you to automate tasks and create custom plugins. In this tutorial, we'll use QgsLayoutExporter() class to export layouts as images, PDFs, and SVGs. Whether you're a GIS professional or a Python developer, you'll find this tutorial helpful to enhance your mapping skills.

We use the ***QgsLayoutExporter()*** class to export a layout that we opened:

```python
manager = QgsProject.instance().layoutManager()
print(manager.printLayouts())
  
layout = manager.layoutByName("Layout1")
```

We use the QgsLayoutExporter() class to export to image, SVG, and PDF:

```python
exporter = QgsLayoutExporter(layout)
```

Export to PNG image:

```python
exporter.exportToImage("D:/Python_QGIS/Layout1.png", QgsLayoutExporter.ImageExportSettings())
```

![Layout1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623514728268/nte6Udvfo.png align="left")

Export to PDF:

```python
exporter.exportToPdf("D:/Python_QGIS/Layout1.pdf", QgsLayoutExporter.PdfExportSettings())
```

Export to SVG image:

```python
exporter.exportToSvg("D:/Python_QGIS/Layout1.svg", QgsLayoutExporter.SvgExportSettings())
```

Use a for loop to export the layout:

```python
for layout in manager.printLayouts():
    exporter = QgsLayoutExporter(layout)
    exporter.exportToImage("D:/Python_QGIS/Image2.png".format(layout.name()),
        QgsLayoutExporter.ImageExportSettings())
```

In conclusion, this tutorial provides a step-by-step guide on how to easily print maps using PyQGIS. It explains how to use QgsLayoutExporter() class to export layouts as images, PDFs, and SVGs. By following this tutorial, GIS professionals and Python developers can enhance their mapping skills and automate tasks. Overall, this tutorial is a helpful resource for anyone looking to improve their knowledge of map printing with PyQGIS.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content