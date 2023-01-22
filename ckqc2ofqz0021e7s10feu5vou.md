# 22- Change main title of the software

Change the main title of QGIS to any name:
```
title = iface.mainWindow().windowTitle()
my_title = title.replace('QGIS', 'QGIS of SmartRS')
iface.mainWindow().setWindowTitle(my_title)
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>