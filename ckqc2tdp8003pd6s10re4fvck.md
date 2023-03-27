---
title: "25- Customize QGIS Icon with PyQGIS: Step-by-Step Guide"
datePublished: Fri Jun 25 2021 08:32:26 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2tdp8003pd6s10re4fvck
slug: 25-customize-qgis-icon-with-pyqgis-step-by-step-guide
tags: tutorial, programming-blogs, python, learning, gis

---

Learn how to customize the QGIS icon using PyQGIS with this step-by-step guide. Follow along as we show you how to download the icon image, import the necessary module, specify the icon name and directory, and create an instance of the QIcon class. You'll also learn how to set the QGIS window icon to the QIcon instance using Python. Whether you're a GIS professional or a Python developer, this tutorial will help you add a personal touch to your QGIS application.

Download the [**QGIS icon image**](https://github.com/Azad77/Python_qgis/blob/main/Data/qgis_orange.png).

Import the `os` module:

```python
import os
```

Specify the icon name, directory, and file path:

```python
icon = 'qgis_orange.png'
data_dir = os.path.join(os.path.expanduser('~'), 'D://', 'Python_QGIS')
icon_path = os.path.join(data_dir, icon)
```

Create an instance of the QIcon class:

```python
icon = QIcon(icon_path)
```

Set the QGIS window icon to the QIcon instance:

```python
iface.mainWindow().setWindowIcon(icon)
```

Here's the overall code:

```python
# import os module
import os

# specify the name of the icon
icon = 'qgis_orange.png'

# specify the data directory where the icon file is stored
data_dir = os.path.join(os.path.expanduser('~'), 'D://', 'Python_QGIS')

# create the path to the icon file
icon_path = os.path.join(data_dir, icon)

# create an instance of the QIcon class using the icon path
icon = QIcon(icon_path)

# set the QGIS window icon to the QIcon instance
iface.mainWindow().setWindowIcon(icon)
```

In conclusion, customizing the QGIS icon using PyQGIS is a straightforward process that can help add a personal touch to your QGIS application. By following the step-by-step guide provided in this article, you can download the icon image, import the necessary module, specify the icon name and directory, and create an instance of the QIcon class. You'll also learn how to set the QGIS window icon to the QIcon instance using Python. Whether you're a GIS professional or a Python developer, this tutorial can be a valuable resource to help you customize your QGIS icon.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content