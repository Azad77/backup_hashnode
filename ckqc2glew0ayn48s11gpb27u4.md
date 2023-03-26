---
title: "17- Writing your processing script in PyQGIS"
datePublished: Fri Jun 25 2021 08:22:30 GMT+0000 (Coordinated Universal Time)
cuid: ckqc2glew0ayn48s11gpb27u4
slug: 17-writing-your-processing-script-in-pyqgis
tags: programming-blogs, python, learning, gis

---

Are you tired of manually processing your GIS data? Do you want to learn how to automate the process using PyQGIS? Look no further! In this article, we will guide you through the steps of creating your processing script in PyQGIS.

Firstly, let's look at some common tasks that can be automated using PyQGIS. These tasks include data conversion, spatial analysis, and map creation. By automating these tasks, you can save time and effort in your GIS projects, allowing you to focus on more important tasks.

To get started with creating your processing script in PyQGIS, follow these steps:

1. Open QGIS and click on *Processing* in the Menu Toolbar, then click on *Toolbox*.
    
2. In the Script Editor, choose "Create new script from template".
    
3. Edit the template to customize the script to your needs. You can use Python code to automate tasks such as loading data, performing spatial analysis, and exporting maps.
    
4. Save your script for future use.
    

It's important to note that creating a processing script in PyQGIS requires some knowledge of Python programming. However, even if you're new to Python, there are many resources available online to help you get started.

By automating GIS data processing using PyQGIS, you can greatly enhance your productivity and efficiency in GIS projects. This skill is particularly useful for professionals in industries such as urban planning, environmental science, and natural resource management.

In QGIS Menu Toolbar click on *Processing* then click on *Toolbox*. Next, in Script Editor, choose "Create new script from template". You can edit it and save it as your script like this example:

![Script_Editor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623886437363/PnAAfYtOR.png align="left")

```python
# Import necessary modules
from qgis.PyQt.QtCore import QCoreApplication
from qgis.core import (QgsProcessing,
                       QgsFeatureSink,
                       QgsProcessingException,
                       QgsProcessingAlgorithm,
                       QgsProcessingParameterFeatureSource,
                       QgsProcessingParameterFeatureSink,
                       QgsMarkerSymbolLayer,
                       QgsMarkerSymbol)
from qgis import processing


class ExampleProcessingAlgorithm(QgsProcessingAlgorithm):

    INPUT = 'INPUT'
    INPUT_PT = 'INPUT_PT'
    OUTPUT = 'OUTPUT'

    def tr(self, string):

        return QCoreApplication.translate('Processing', string)

    def createInstance(self):
        return ExampleProcessingAlgorithm()

    # Name of the algorithm as it appears in the Toolbox
    def name(self):
        return 'myscript'

    # Display name of the algorithm
    def displayName(self):
        return self.tr('My Processing Script')

    # Group name of the algorithm
    def group(self):
        return self.tr('Example scripts')

    # Group id of the algorithm
    def groupId(self):
        return 'examplescripts'

    # Short description of the algorithm
    def shortHelpString(self):
        return self.tr("Example algorithm short description")

    # Initialize the algorithm
    def initAlgorithm(self, config=None):
        
        # Add input parameter for the input layer
        self.addParameter(
            QgsProcessingParameterFeatureSource(
                self.INPUT,
                self.tr('Input layer'),
                [QgsProcessing.TypeVectorAnyGeometry]
            )
        )

        # Add input parameter for the point layer
        self.addParameter(
            QgsProcessingParameterFeatureSource(
                self.INPUT_PT,
                self.tr('Point layer'),
                [QgsProcessing.TypeVectorPoint]
            )
        )
      
        # Add output parameter for the output layer
        self.addParameter(
            QgsProcessingParameterFeatureSink(
                self.OUTPUT,
                self.tr('Output layer')
            )
        )

    # Process the algorithm
    def processAlgorithm(self, parameters, context, feedback):
       
        # Get the source input layer
        source = self.parameterAsSource(
            parameters,
            self.INPUT,
            context
        )

        # Raise an exception if the source layer is invalid
        if source is None:
            raise QgsProcessingException(self.invalidSourceError(parameters, self.INPUT))

        # Get the sink output layer:
        (sink, dest_id) = self.parameterAsSink(
            parameters,
            self.OUTPUT,
            context,
            source.fields(),
            source.wkbType(),
            source.sourceCrs()
        )

        # Print the CRS of the input layer to the processing log:
        feedback.pushInfo('CRS is {}'.format(source.sourceCrs().authid()))

        # Get the point layer:
        point_layer = self.parameterAsVectorLayer(
            parameters,
            self.INPUT_PT,
            context
            )

        # Create a simple marker symbol and set it as the renderer for the point layer:
        pt_symbol = QgsMarkerSymbol.createSimple({"color": "0,0,255","name": "rectangle"})
        point_layer.renderer().setSymbol(pt_symbol)
        point_layer.triggerRepaint()

        # Raise an exception if the sink output layer is invalid:
        if sink is None:
            raise QgsProcessingException(self.invalidSinkError(parameters, self.OUTPUT))

        # Calculate the total progress percentage
        total = 100.0 / source.featureCount() if source.featureCount() else 0
        features = source.getFeatures()

        for current, feature in enumerate(features):

            if feedback.isCanceled():
                break

            sink.addFeature(feature, QgsFeatureSink.FastInsert)

            feedback.setProgress(int(current * total))

        return {self.OUTPUT: dest_id}
```

To learn more about PyQGIS and GIS data processing, we recommend checking out the QGIS documentation and joining online communities such as the QGIS user group on LinkedIn.

In conclusion, automating GIS data processing using PyQGIS can save a lot of time and effort in GIS projects. With the help of the steps provided in this article, you can easily create and customize your own processing script in PyQGIS. This can greatly enhance your productivity and efficiency in GIS data processing.

> If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content