# 11- Run processing

```
uri = "D:/Python_QGIS/data/KRG_Cities.shp" 
```

Using *run()*
```
processing.run("native:buffer", {'INPUT': uri,
               'DISTANCE': 100.0,
               'SEGMENTS': 10,
               'DISSOLVE': True,
               'END_CAP_STYLE': 0,
               'JOIN_STYLE': 0,
               'MITER_LIMIT': 10,
               'OUTPUT': 'D:/Python_QGIS/data/buffers.shp'})
```

Using *runAndLoadResults()*
```
processing.runAndLoadResults("native:buffer", 
                {'INPUT':uri,
                'DISTANCE':1,
                'SEGMENTS':5,
                'END_CAP_STYLE':0,
                'JOIN_STYLE':0,
                'MITER_LIMIT':2,
                'DISSOLVE':False,
                'OUTPUT':'memory:'})
```