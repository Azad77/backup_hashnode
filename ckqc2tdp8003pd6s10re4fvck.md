# 25- Change the main icon of QGIS

Download icon  [image](https://github.com/Azad77/Python_qgis/blob/main/Data/qgis_orange.png) 
```
import os

icon = 'qgis_orange.png'
data_dir = os.path.join(os.path.expanduser('~'), 'D://', 'Python_QGIS')
icon_path = os.path.join(data_dir, icon)
icon = QIcon(icon_path)
iface.mainWindow().setWindowIcon(icon)
```

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>