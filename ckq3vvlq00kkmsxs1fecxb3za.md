# 22- Change main title of the software

Change the main title of QGIS to any name:
```
title = iface.mainWindow().windowTitle()
my_title = title.replace('QGIS', 'QGIS of SmartRS')
iface.mainWindow().setWindowTitle(my_title)
```