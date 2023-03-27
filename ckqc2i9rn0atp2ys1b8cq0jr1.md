---
title: "18- Building an Interactive Dialog Box in PyQGIS: A Step-by-Step Guide"
datePublished: Fri Jun 25 2021 08:23:48 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2i9rn0atp2ys1b8cq0jr1
slug: 18-building-an-interactive-dialog-box-in-pyqgis-a-step-by-step-guide
tags: tutorial, programming-blogs, python, learning, gis

---

Are you tired of manually asking users if they want to save changes in QGIS? Look no further than this step-by-step guide on how to build an interactive dialog box! With the help of PyQGIS, you can create a user-friendly experience that saves time and effort. Follow along and learn how to streamline your workflow with this handy tool.

Building a dialog box to ask if users want to save changes:

```python
# import the necessary modules
from PyQt5.QtWidgets import QMessageBox

# create a QMessageBox instance
qmb = QMessageBox()

# set the text displayed on the QMessageBox:
qmb.setText('Want to save your changes?')

# set the standard buttons for the QMessageBox (Save, Discard, and Cancel):
qmb.setStandardButtons(QMessageBox.Save | QMessageBox.Discard | QMessageBox.Cancel)

# execute the QMessageBox and store the return value:
return_value = qmb.exec()

# check the return value and print a message based on the button pressed:
if return_value == QMessageBox.Save:
    print("You pressed Save")
elif return_value == QMessageBox.Discard:
    print("You pressed Discard")
else:
    print('You pressed Cancel')
```

In conclusion, building an interactive dialog box in PyQGIS can greatly improve the user experience and streamline workflows in QGIS. With this step-by-step guide, users can easily create a dialog box to prompt users to save changes, saving time and effort. By utilizing PyQGIS, users can create a more efficient and user-friendly experience in QGIS.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content