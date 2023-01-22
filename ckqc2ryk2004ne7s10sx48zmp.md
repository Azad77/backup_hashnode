# 24- Add a time button to a toolbar

Download icon  [image](https://github.com/Azad77/Python_qgis/blob/main/Data/time.png)  of time
```
import os
from datetime import datetime

# path of icon
icon = 'time.png'
data_dir = os.path.join(os.path.expanduser('~'), 'D://', 'Python_QGIS')
icon_path = os.path.join(data_dir, icon)

# define Baghdad local time
def WhatTime():
    tz_Ba = pytz.timezone('Asia/Baghdad') 
    now = datetime.now(tz_Ba)
    current_time = now.strftime("%H:%M:%S")
    iface.messageBar().pushInfo('Baghdadt Time', current_time)
    
action = QAction('What time is it?')
action.triggered.connect(WhatTime)
action.setIcon(QIcon(icon_path))
iface.addToolBarIcon(action)
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>

