# 26- Creating your plugin

The first requirement for plugins is **metadata.txt**.
<p>Use a text editor to create a metadata file:<p/>

```
[general]
name=TestPlugin
email=azad.rasul@soran.edu.iq
author=Azad Rasul
qgisMinimumVersion=3.0
description=This is an example plugin for greeting the world.
version=version 1.0 
```
save it as "metadata" text document.

<p>Second file is called "__init__".py which include *classFactory()* method.<p/>
You can use Python to create __init__ file
![_init_.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624029301411/BOurKJv14.png)



```
from .mainPlugin import TestPlugin
def classFactory(iface):
  return TestPlugin(iface)
```

Third necessary file contains the main logic of the plugin. It must have __init__(), initGui, and unload method. We name it *mainPlugin.py*  file that includes:

```
import os
import sys
import inspect
from PyQt5.QtWidgets import QAction
from PyQt5.QtGui import QIcon

cmd_folder = os.path.split(inspect.getfile(inspect.currentframe()))[0]
###
class TestPlugin:

  def __init__(self, iface):
    self.iface = iface

  def initGui(self):
    icon = os.path.join(os.path.join(cmd_folder, 'logo.png'))
    self.action = QAction(QIcon(icon), 'Test plugins', self.iface.mainWindow())
    self.action.triggered.connect(self.run)
    # add toolbar button and menu item
    self.iface.addToolBarIcon(self.action)
    self.iface.addPluginToMenu("&Test plugins", self.action)


  def unload(self):
    # remove the plugin menu item and icon
    self.iface.removePluginMenu("&Test plugins", self.action)
    self.iface.removeToolBarIcon(self.action)
    del self.action

  def run(self):
    # create and show a configuration dialog or something similar
    self.iface.messageBar().pushMessage('Hello from TestPlugin!')

```

Save these three files and a logo in one folder and name it "TestPlugin" or the name of the plugin. 

Then, copy the file and past it in QGIS 3 Plugins directory. On my computer it is:
<p>C:\Users\Azad\AppData\Roaming\QGIS\QGIS3\profiles\default\python\plugins<p/>

Restart QGIS software and now you can see your "TestPlugin" plugin in the list of installed plugins.

Another method is to use "Plugin Builder" to create your template plugin then modify it.