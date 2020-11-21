---
title:  "Desarrollando un plugin de procesamiento en QGIS"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202011_procesingplugin/06mytools.png" 
categories: 
  - 2020
tags:
  - python
  - qgis
  - pyqgis
  - plugin
---
Cada día que pasa usando [QGIS](https://www.qgis.org/es/site/), me sorprende más. Su aplicación a nivel profesional no tiene que envidiar a cualquier GIS del mercado. **Las posibilidades de desarrollo e integración de herramientas y complementos usando Python, la API [PyQGIS](https://docs.qgis.org/3.16/en/docs/pyqgis_developer_cookbook/index.html) y PyQt son enormes**.

En la siguiente entrada quiero mostrar **cómo integrar procesos creados con el Modelador gráfico de QGIS dentro de un plugin**.


## Creamos un complemento con Plugin Builder

Como el objetivo es integrar opciones de procesamiento en un complemento ya existente, usamos **Plugin Builder** para generar de forma rápida nuestro plugin. Os recomiendo también instalar **Plugin Reloader**.

El complemento no va a tener ninguna funcionalidad, solo la que trae por defecto, que añade un icono a la barra de herramientas. Al hacer clic sobre el botón se abre un panel sencillo información.


El complemento se va a llamar **MyTools**. Será el nombre que tendrá la **clase**. 

El **módulo**, siguiendo criterios correctos para la asignación de nombres en Python, se llamará nombre **my_tools**. 

![01pluginbuilder.png](/images/blog/202011_procesingplugin/01pluginbuilder.png)


Vamos también a iniciar **Git** en nuestro proyecto y así tener controlados los cambios y versiones. 

Dentro de la carpeta añadimos también un archivo *.gitignore* para proyectos Python. Descubrí hace poco el complemento [".gitignore Generator"](https://marketplace.visualstudio.com/items?itemName=piotrpalarz.vscode-gitignore-generator) para Visual Studio Code, una joya para decirle a Git qué archivos o directorios completos debe ignorar y no subir al repositorio de código.

Movemos la carpeta del proyecto a la ruta de complementos de nuestro perfil de QGIS y ya tendremos nuestro "super potente" complemento.

![03_pluginOk.gif](/images/blog/202011_procesingplugin/03_pluginOk.gif)

## Añadiendo procesos a MyTools

Plugin Builder tiene una opción que permite crear proyectos para añadir geoprocesos a la Caja de herramientas. Pero en esta ocasión, me parece más interesante poder ver cómo integrar código en un complemento ya existente. Es un buen ejercicio para revisar **cómo se desarrollan e importan módulos en Python**. 

En este sentido, quiero comentar que gracias a las herramientas, complementos de desarrollo y entradas como esta, cada vez es más sencillo que un usuario con interés pueda crear complementos. 

Pero desde el punto de vista profesional, y para aquellas personas que no vengan directamente de ciclos o carreras vinculadas con la programación, **es fundamental ir adquiriendo una buena base teórica sobre el lenguaje con el que se trabaja**.

Esto para mi, es fundamental. **Entender los fundamentos de la programación orientada a objetos (POO)** te permite da un salto cualitativo en proyectos basados en Python o Javascript.

El primer paso es crear un archivo que instancie la la clase *QgsProcessingProvider* de la API PyQGIS. Usaremos esta clase para crear un proveedor de geoalgoritmos. 

Podemos ver ejemplos de proveedores que ya vienen por defecto en QGIS dentro de la Caja de Herramientas. Además de QGIS, tenemos SAGA, GRASS, GDAL y todos los que nos añadan los complementos que instalemos.

![Provedores de procesos de QGIS](/images/blog/202011_procesingplugin/04provider.png)

Dentro de este archivo Python, que vamos a llamar *my_tools_provider.py*, tendremos las funciones para asignar nombre al proveedor, añadir una descripción, asignarle un icono y sobre todo, la configuración de herramienta procesamiento que vamos a añadir.

```python
# my_tools_provider.py

from processing_provider.example_processing_algorithm import \
    ExampleProcessingAlgorithm
from qgis.core import QgsProcessingProvider

from PyQt5.QtGui import QIcon
from os import path

class MyToolsProvider(QgsProcessingProvider):

    def loadAlgorithms(self, *args, **kwargs):
        # self.addAlgorithm(MyOtherAlgorithm())

    def id(self, *args, **kwargs):
        """The ID of your plugin, used for identifying the provider.
        """
        return 'mytools'

    def name(self, *args, **kwargs):
        """The human friendly name of your plugin in Processing.
        """
        return self.tr('My Tools')

    def icon(self):
        """Should return a QIcon which is used for your provider inside
        the Processing toolbox.
        """
       return QIcon(path.dirname(__file__) + '/icon.png')

    def longName(self):
        """
        Returns the a longer version of the provider name, which can include
        extra details such as version numbers.
        """

        return self.name('Collection of my custom tools')
```

## Módulo de procesos.

Para ir añadiendo  procesos en nuestro proveedor, vamos a generar un nuevo módulo Python dentro de la carpeta de proyecto que llamaremos **tools**. Esta carpeta va a almacenar los archivos de cada uno de los procesos que creemos.

El paquete debe contener el archivo **__init__.py** y el otro archivo *clip_layer.py* con el código del proceso.

En *init* realizaremos la importación del archivo con el proceso.

```python
# __init__.py

# -*- coding: utf-8 -*-

from .clip_layer import ClipLayer

```

Dentro de *clip_layer.py* incluiremos el proceso generado en esta ocasión desde el Modelador Gráfico. Es un simple recorte a capa vectorial que no sirve de ejemplo. 

![Modelo de QGIS](/images/blog/202011_procesingplugin/05model_builder.png)

Es importante fijarse en las funciones que definen el nombre o el grupo donde se insertará el proceso en el caso de que tengamos varios.

```python
# clip_layer.py

# -*- coding: utf-8 -*-
__author__ = 'Patricio Soriano @sigdeletras'
__date__ = '2020-11-15'

import processing
from qgis.core import (QgsProcessing, QgsProcessingAlgorithm,
                       QgsProcessingMultiStepFeedback,
                       QgsProcessingParameterFeatureSink,
                       QgsProcessingParameterVectorLayer)


class ClipLayer(QgsProcessingAlgorithm):

    def initAlgorithm(self, config=None):
        self.addParameter(QgsProcessingParameterVectorLayer(
            'CapaARecortar', 'Capa a recortar', defaultValue=None))
        self.addParameter(QgsProcessingParameterVectorLayer(
            'CapaRecorte',
            'Capa Recorte',
            types=[QgsProcessing.TypeVectorPolygon], defaultValue=None))
        self.addParameter(QgsProcessingParameterFeatureSink(
            'CapaRecortada',
            'Capa recortada',
            type=QgsProcessing.TypeVectorAnyGeometry,
            createByDefault=True,
            defaultValue=None))

    def processAlgorithm(self, parameters, context, model_feedback):
        feedback = QgsProcessingMultiStepFeedback(1, model_feedback)
        results = {}
        outputs = {}

        # Cortar
        alg_params = {
            'INPUT': parameters['CapaARecortar'],
            'OVERLAY': parameters['CapaRecorte'],
            'OUTPUT': parameters['CapaRecortada']
        }
        outputs['Cortar'] = processing.run(
            'native:clip', alg_params,
            context=context,
            feedback=feedback,
            is_child_algorithm=True)
        results['CapaRecortada'] = outputs['Cortar']['OUTPUT']
        return results

    def name(self):
        return 'Recorte Capa'

    def displayName(self):
        return 'Recorte Capa'

    def group(self):
        return 'Vectoriales'

    def groupId(self):
        return 'vector'

    def createInstance(self):
        return ClipLayer()
```

El último paso será añadir el algoritmo en el proveedor, importando la clase **ClipLayer** desde el nuevo paquete, y añadiendolo dentro de la función *loadAlgorithms()*

```python
# my_tools_provider.py
...

from .tools.clip_layer import ClipLayer


class MyToolsProvider(QgsProcessingProvider):

    def loadAlgorithms(self, *args, **kwargs):
        self.addAlgorithm(ClipLayer())

...
```

## Cargando nuestro proveedor

Si recargamos el complemento en este momento podemos comprobar que no se han añadido nuestras herramientas personalizadas. Esto se debe a que no hemos indicado en el archivo del complemento la función para que se cargue.

Para ello vamos a añadir en *my_tools.py* la función que se encarga de ello. Debemos también importar los módulos del *core* de QGIS correspondiente.

```python
# my_tools.py
...
    def initProcessing(self):
        # Add the processing provider
        self.my_tools_provider = MyToolsProvider()
        QgsApplication.processingRegistry().addProvider(self.my_tools_provider)
...
```

Y para terminar, incluimos la función dentro del constructor del complemento encargado de iniciarlo.

```python
# my_tools.py

...
class MyTools:

    def __init__(self, iface):

        self.initProcessing()
...

```

![06mytools.png](/images/blog/202011_procesingplugin/06mytools.png)

Tenéis el código completo del ejemplo en mi [repositorio de GitHub](https://github.com/sigdeletras/qgis_processing_plugin_example).

## ¿Matando moscas a cañonazos?

Como he comentado al principio, **QGIS es grande y su licencia abierta permite realizar este tipo de desarrollos sin problema**. 

El ejemplo que he comentado es muy básico, no necesitamos un complemento para hacer un simple 'Clip' una capa. Es más, a nivel de usuario esta misma posibilidad la podemos suplir con los modelos.

Pero **desde el punto de vista profesional**, o a nivel corporativo, las opciones son muchas. **Tener un plugin propio con la recopilación de los procesos que más se usan dentro de la empresa y poder controlar versiones y actualizaciones, es un desarrollo a tener en cuenta**.

De igual manera, gracias al paquetizado de procesos complejos, **podemos dar acceso a usuarios no avanzados, y hacer más accesible este tipo de herramientas**.

## Referencias

- [Documentación oficial de QGIS](https://docs.qgis.org/3.16/en/docs/pyqgis_developer_cookbook/processing.html)
- [Building a Processing Plugin (QGIS3)](https://www.qgistutorials.com/en/docs/3/processing_python_plugin.html) de la web QGIS Tutorials and Tips de Ujaval Gandhi.


