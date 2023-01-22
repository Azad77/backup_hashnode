# 21- Add a new menu item to the QGIS software

```
import webbrowser

def open_website():
    webbrowser.open('https://smartrs.hashnode.dev/series/learning-python-qgis')
    
website_action = QAction('Go to Learning Python QGIS')
website_action.triggered.connect(open_website)
iface.helpMenu().addSeparator()
iface.helpMenu().addAction(website_action)
```