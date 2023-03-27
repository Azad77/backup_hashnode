---
title: "24- Enhance Your PyQGIS Toolbar with a Time Button: A Step-by-Step Guide"
datePublished: Fri Jun 25 2021 08:31:20 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2ryk2004ne7s10sx48zmp
slug: 24-enhance-your-pyqgis-toolbar-with-a-time-button-a-step-by-step-guide
tags: tutorial, programming-blogs, python, learning, gis

---

Learn how to enhance your PyQGIS toolbar with a time button by following this step-by-step guide. With the help of necessary modules and code, you can create a QGIS toolbar icon that displays the current time when clicked. Download the time icon and define the path to the icon to get started with this tutorial. Follow along with the instructions to create your own time button and upgrade your PyQGIS toolbar.

First, download the time icon [**image**](https://github.com/Azad77/Python_qgis/blob/main/Data/time.png).

Then, import the necessary modules:

```python
import os
import pytz
from datetime import datetime
```

Next, define the path to the icon:

```python
icon = 'time.png'
data_dir = os.path.join(os.path.expanduser('~'), 'D://', 'Python_QGIS')
icon_path = os.path.join(data_dir, icon)
```

Next, define Baghdad local time by creating the "WhatTime" function:

```python
def WhatTime():
    tz_Ba = pytz.timezone('Asia/Baghdad') 
    now = datetime.now(tz_Ba)
    current_time = now.strftime("%H:%M:%S")
    iface.messageBar().pushInfo('Baghdad Time', current_time)
```

Finally, create a QGIS toolbar icon that displays the current time when clicked:

```python
action = QAction('What time is it?')
action.triggered.connect(WhatTime)
action.setIcon(QIcon(icon_path))
iface.addToolBarIcon(action)
```

Here's the overall code:

```python
# Import the necessary modules:
import os
import pytz
from datetime import datetime

Define the path to the icon:
icon = 'time.png'
data_dir = os.path.join(os.path.expanduser('~'), 'D://', 'Python_QGIS')
icon_path = os.path.join(data_dir, icon)

# Define Baghdad local time
def WhatTime():
    tz_Ba = pytz.timezone('Asia/Baghdad') 
    now = datetime.now(tz_Ba)
    current_time = now.strftime("%H:%M:%S")
    iface.messageBar().pushInfo('Baghdad Time', current_time)

# Create a QGIS toolbar icon that displays the current time when clicked:    
action = QAction('What time is it?')
action.triggered.connect(WhatTime)
action.setIcon(QIcon(icon_path))
iface.addToolBarIcon(action)
```

In conclusion, this step-by-step guide provides a clear and concise tutorial on how to enhance your PyQGIS toolbar with a time button. By following the instructions and using the necessary modules and code, users can create a QGIS toolbar icon that displays the current time when clicked. This feature can be useful for those who need to keep track of time while working with PyQGIS. Overall, this tutorial is a useful resource for those looking to upgrade their PyQGIS toolbar.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content