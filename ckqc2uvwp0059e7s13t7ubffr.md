---
title: "26- Creating QGIS Plugins: A Step-by-Step Guide"
datePublished: Fri Jun 25 2021 08:33:36 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2uvwp0059e7s13t7ubffr
slug: 26-creating-qgis-plugins-a-step-by-step-guide
tags: tutorial, programming-blogs, python, learning, gis

---

If you're looking to create QGIS plugins, then you've come to the right place! In this step-by-step guide, we'll show you how to create your own plugin by creating essential files such as metadata.txt and [mainPlugin.py](http://mainPlugin.py), as well as how to use Python to create the **init**.py file. We'll also walk you through how to install your plugin and provide a tip on using the Plugin Builder to create a template for your plugin. Follow these instructions to create your own QGIS plugin and take your GIS analysis to the next level!

The first requirement for plugins is **metadata.txt**.

Use a text editor to create a metadata file:

```plaintext
[general]
name=TestPlugin
email=azad.rasul@soran.edu.iq
author=Azad Rasul
qgisMinimumVersion=3.0
description=This is an example plugin for greeting the world.
version=version 0.1
```

save it as a "metadata" text document.

The second file is called "\_\_init\_\_".py which includes the **classFactory()** method.

You can use Python to create \_\_init\_\_ file

!\[\_init\_.png\](https://cdn.hashnode.com/res/hashnode/image/upload/v1624029301411/BOurKJv14.png)

```python
from .mainPlugin import TestPlugin
def classFactory(iface):
  return TestPlugin(iface)
```

The third necessary file contains the main logic of the plugin. It must have **init**(), initGui, and unload method. We name it *mainPlugin.py* file that includes:

```python
import os
import inspect
from PyQt5.QtWidgets import QAction
from PyQt5.QtGui import QIcon

# get the directory containing this script
cmd_folder = os.path.split(inspect.getfile(inspect.currentframe()))[0]

# define the TestPlugin class
class TestPlugin:

  def __init__(self, iface):
    self.iface = iface

  # initialize the plugin interface
  def initGui(self):
    # get the path to the plugin icon
    icon = os.path.join(os.path.join(cmd_folder, 'logo.png'))

    # create a new QAction with the plugin icon and label
    self.action = QAction(QIcon(icon), 'TestPlugin', self.iface.mainWindow())

    # connect the action to the run() method
    self.action.triggered.connect(self.run)

    # add the action to the toolbar and menu
    self.iface.addToolBarIcon(self.action)
    self.iface.addPluginToMenu("&TestPlugin", self.action)

  # unload the plugin
  def unload(self):
    # remove the action from the toolbar and menu
    self.iface.removePluginMenu("&TestPlugin", self.action)
    self.iface.removeToolBarIcon(self.action)

    # delete the action object
    del self.action

  # run the plugin
  def run(self):
    # display a message in the QGIS message bar
    self.iface.messageBar().pushMessage('Hello from TestPlugin!')
```

Save these three files and a logo in one folder and name it "TestPlugin" or the name of the plugin.

Then, copy the file and paste it into QGIS 3 Plugins directory. On my computer it is:

C:\\Users\\Azad\\AppData\\Roaming\\QGIS\\QGIS3\\profiles\\default\\python\\plugins

Restart QGIS software and now you can see your "TestPlugin" plugin in the list of installed plugins.

Another method is to use "Plugin Builder" to create your template plugin and then modify it.

In conclusion, creating QGIS plugins can seem like a daunting task, but with the help of this step-by-step guide, anyone can create their own customized plugin. By following the instructions provided, users can create the necessary files, such as metadata.txt and [mainPlugin.py](http://mainPlugin.py), and use Python to create the [**init**.py](http://init.py) file. The article also provides a tip on using the Plugin Builder to create a template for the plugin. With the plugin created and installed, users can take their GIS analysis to the next level.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content