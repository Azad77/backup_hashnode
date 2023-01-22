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

<blockquote>
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>
</blockquote>