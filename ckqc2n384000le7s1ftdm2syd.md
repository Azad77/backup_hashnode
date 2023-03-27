---
title: "21- Add a new menu item to the QGIS software"
datePublished: Fri Jun 25 2021 08:27:33 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2n384000le7s1ftdm2syd
slug: 21-add-a-new-menu-item-to-the-qgis-software-1
tags: tutorial, programming-blogs, python, learning, gis

---

```python
import webbrowser

def open_website():
    webbrowser.open('https://smartrs.blog/series/pyqgis-basics')
    
website_action = QAction('Go to: Introduction to PyQGIS')
website_action.triggered.connect(open_website)
iface.helpMenu().addSeparator()
iface.helpMenu().addAction(website_action)
```

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content