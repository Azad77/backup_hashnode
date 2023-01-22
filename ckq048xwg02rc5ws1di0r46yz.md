# 17- Writing your processing script

In QGIS Menu Toolbar click on *Processing* then click on *Toolbox*. Next, in Script Editor, choose "Create new script from template". You can edit it and save it as your script like this example:

![Script_Editor.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1623886437363/PnAAfYtOR.png)
```
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

    def name(self):
        return 'myscript'

    def displayName(self):
        return self.tr('My Script')

    def group(self):
        return self.tr('Example scripts')

    def groupId(self):
        return 'examplescripts'

    def shortHelpString(self):
        return self.tr("Example algorithm short description")

    def initAlgorithm(self, config=None):
        

        self.addParameter(
            QgsProcessingParameterFeatureSource(
                self.INPUT,
                self.tr('Input layer'),
                [QgsProcessing.TypeVectorAnyGeometry]
            )
        )
        self.addParameter(
            QgsProcessingParameterFeatureSource(
                self.INPUT_PT,
                self.tr('Point layer'),
                [QgsProcessing.TypeVectorPoint]
            )
        )
      

        self.addParameter(
            QgsProcessingParameterFeatureSink(
                self.OUTPUT,
                self.tr('Output layer')
            )
        )

    def processAlgorithm(self, parameters, context, feedback):
       

        source = self.parameterAsSource(
            parameters,
            self.INPUT,
            context
        )


        if source is None:
            raise QgsProcessingException(self.invalidSourceError(parameters, self.INPUT))

        (sink, dest_id) = self.parameterAsSink(
            parameters,
            self.OUTPUT,
            context,
            source.fields(),
            source.wkbType(),
            source.sourceCrs()
        )

        feedback.pushInfo('CRS is {}'.format(source.sourceCrs().authid()))
        pt_lyr = self.parameterAsVectorLayer(
            parameters,
            self.INPUT_PT,
            context
            )
            
        pt_symbol = QgsMarkerSymbol.createSimple({"color": "0,0,255","name": "rectangle"})
        pt_lyr.renderer().setSymbol(pt_symbol)
        pt_lyr.triggerRepaint()

        if sink is None:
            raise QgsProcessingException(self.invalidSinkError(parameters, self.OUTPUT))


        total = 100.0 / source.featureCount() if source.featureCount() else 0
        features = source.getFeatures()

        for current, feature in enumerate(features):

            if feedback.isCanceled():
                break



            sink.addFeature(feature, QgsFeatureSink.FastInsert)



            feedback.setProgress(int(current * total))

        if False:
            buffered_layer = processing.run("native:buffer", {
                'INPUT': dest_id,
                'DISTANCE': 1.5,
                'SEGMENTS': 5,
                'END_CAP_STYLE': 0,
                'JOIN_STYLE': 0,
                'MITER_LIMIT': 2,
                'DISSOLVE': False,
                'OUTPUT': 'memory:'
            }, context=context, feedback=feedback)['OUTPUT']


        return {self.OUTPUT: dest_id}
```
