# 12- Map Printing

![Layout.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623514088236/0S5bBpoF3.png)

We use *QgsLayoutExporter()*, class, to export a layout that we opened
```
manager = QgsProject.instance().layoutManager()
print(manager.printLayouts())
  
layout = manager.layoutByName("Layout1")
```
we use *QgsLayoutExporter()* to export to image, SVG, and PDF

```
exporter = QgsLayoutExporter(layout)
```

Export to png image
```
exporter.exportToImage("D:/Python_QGIS/Layout1.png", QgsLayoutExporter.ImageExportSettings())
```

![Layout1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623514728268/nte6Udvfo.png)
Export to pdf
```
exporter.exportToPdf("D:/Python_QGIS/Layout1.pdf", QgsLayoutExporter.PdfExportSettings())
```
Export to svg image
```
exporter.exportToSvg("D:/Python_QGIS/Layout1.svg", QgsLayoutExporter.SvgExportSettings())
```

Using for loop to export layout
```
for layout in manager.printLayouts():
    exporter = QgsLayoutExporter(layout)
    exporter.exportToImage("D:/Python_QGIS/Image2.png".format(layout.name()),
        QgsLayoutExporter.ImageExportSettings())
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>