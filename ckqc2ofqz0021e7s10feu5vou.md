---
title: "22- Customize Your QGIS Window Title with PyQGIS"
datePublished: Fri Jun 25 2021 08:28:36 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2ofqz0021e7s10feu5vou
slug: 22-customize-your-qgis-window-title-with-pyqgis
tags: tutorial, programming-blogs, python, learning, gis

---

Learn how to customize the title of your QGIS window using PyQGIS in this tutorial. With just a few lines of code, you can change the default title to any name you want, such as "My QGIS". Follow the step-by-step instructions and sample code to get started.

To get the current title of the QGIS window:

```python
title = iface.mainWindow().windowTitle()
```

To create a new title by replacing the substring 'QGIS' with 'My QGIS':

```python
my_title = title.replace('QGIS', 'My QGIS')
```

To set the new title to the QGIS window:

```python
iface.mainWindow().setWindowTitle(my_title)
```

Here's the overall code:

```python
title = iface.mainWindow().windowTitle()
my_title = title.replace('QGIS', 'My QGIS')
iface.mainWindow().setWindowTitle(my_title)
```

In conclusion, this tutorial provides a simple and easy-to-follow guide on how to customize the title of the QGIS window using PyQGIS. By following the step-by-step instructions and sample code provided in the article, users can easily change the default title of the QGIS window to any name they want. This feature can be useful for users who want to personalize their QGIS environment or create custom branding for their projects. Overall, this tutorial is a great resource for anyone looking to customize their QGIS window title using PyQGIS.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content