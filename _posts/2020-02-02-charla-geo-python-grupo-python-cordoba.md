---
title:  "Charla Geo & Python en la reunión de Python Córdoba (ES)"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202003_geopyhton/giphy.gif" 
categories: 
  - 2020
tags:
  - python
---

Se me había quedado en el tintero hacer una entrada sobre una charla que di en octubre del año pasado en los eventos organizados por el grupo de [Python Córdoba (ES)](https://www.meetup.com/es-ES/Meetup-de-Python-en-Cordoba/). Este grupo, dinamizado por [Javier Aguirre](https://twitter.com/javaguirre), forma parte de las comunidades *"tech"* que se mueven por Córdoba.

![Geopython](https://media.giphy.com/media/jRZGMR8SVNfYjjdw3k/giphy.gif)

En el grupo de Whatsapp se me propuso dar una charla sobre la aplicación de Python en el mundo geo, y como no puedo resistirme a este tipo de cosas me lié la manta a la cabeza y me puse a ello. Aunque Python es el primer lenguaje que usé, la verdad es que llevaba tiempo sin tocarlo, y menos para dar una charla donde mucho de los asistentes tienen mucha más experiencia que yo. Esto siempre de un poco de respeto, sobre todo pensando en lo que puedes aportar para no hacer perder el tiempo a la gente. Creo que al final se quedó algo decente. Al menos a mi me sirvió para hacer un repaso general a este tema y profundizar algo más en cuestiones que no he tocado.

## Contextualizando...

Como he comentado, a este tipo de charlas asiste gente que ya sabe de lo que se habla. Pero el grupo de Python Córdoba, debido sobre todo a los múltiples campos de aplicación que tiene este lenguaje, es bastante diverso pudiéndo encontrar gente que se dedica a la biología, ingeniería, arquitectura o documentación que, de alguna u otra manera, manejan o tienen interés en usar Python en su ámbito profesional.

Por todo esto, pensé que sería bueno hacer una introducción de porqué Python es tan interesante para un campo amplio de usuarios y  jugar un poco entre los motivos de interés para perfil desarrollador  y otro no desarrollador. Quisé también hacer un breve repaso a qué es esto de lo "geo", comentando aspectos básicos sobre las características de la información geográfica (coordenadas, sistemas de representación, ráster, vectorial, proyecciones...)

## ¿Es Python un lenguaje Geo?

Tras estas primeras láminas, me apoyé en el listado de funcionalidades básicas que debe cumplir un SIG definidas Víctor Olaya [(@volayaf)] (https://twitter.com/volayaf) en su [Libro Libre SIG](https://volaya.github.io/libro-sig/) para revisar si Python, como lenguaje de programación, permite realizar las tareas básicas de cada una de estas funcionalidades. Me centré en estas cuatro grandes funcionalidades.

- Entrada/salida de datos.
- Creación/edición. 
- Visualización.
- Análisis. 

## Entrada/salida de datos.

Python ya trae por defecto un conjunto de librerías que nos van a permitir trabajar y crear nuevos conjuntos de datos. Podemos usar las funciones de *sys, os, os.path o shutil* para manejar acceder a la información, trabajar con rutas a ficheros o mover, copiar, cortar archivos. Gracias a *urllib.request* podemos realizar también peticiones HTTP. Y es posible también instalar librerías como [psycopg2](https://pypi.org/project/psycopg2/)para acceder a bases de datos.

Pero como sabemos, los datos geo tienen su propia estructura y formatos por lo que debemos usar librería específicas para poder manejarlos desde Python. Entre las más conocidas se encuentras:

- [GDAL](https://pypi.org/project/GDAL/) Librería para lectura y escritura de formatos de datos geoespaciales vectoriales (OGR) y raster (GDAL)
- [Shapely](https://pypi.org/project/Shapely/) [Fiona]() Manipulación y el análisis de datos vectoriales
- [Rasterio](https://pypi.org/project/rasterio/0.13.2/) Leer, manipular y escribir archivos de tipo ráster.
- [GeoPandas](http://geopandas.org/) Permitir el uso de archivos y operaciones espaciales. 
- [pyproj](https://pypi.org/project/pyproj/)  Interfaz de la librería PROJ4 de OSGeo para proyección y conversión de geometrías entre sistemas de referencia de coordenadas.

![Lectura de un archivo GeoJSON con GeoPandas](/images/blog/202003_geopyhton/geopandas.png)

*Lectura de un archivo GeoJSON con GeoPandas*

## Creación/edición.

Algunas de las librerías anteriores también pueden ser usadas para creación y edición de datos espaciales. Pero desde mi punto de vista esto no significa que gracias a ellas nuestro trabajo vaya a ser ágil. Sin duda para un usuario SIG, es mucho más sencillo realizar un operación de corte (clip) entre capas vectoriales o ráster desde un SIG de escritorio que hacerlo programando. **Pero ¿qué ocurre si esta operación debe realizarse gran cantidad de veces, o sobre cientos de capas?. Es aquí donde Python puede ser de gran ayuda a modo de "navaja suiza"**. Podemos escribir un script o fragmento de código que recoja una serie de variables (rutas, archivos...) y que realice de forma iterativa un conjunto de operaciones (funciones) como pueden ser descomprimir, copiar, renombrar, recortar, reproyectar, geocodificar... Es aquí donde se encuentra la potencia de usar un lenguaje de programación como Python.

![Clip de shapes](/images/blog/202003_geopyhton/ejemplo_clip.png)

*Clip de shapes. [Código en Github](https://github.com/sigdeletras/clipShapesZip)*

## Visualización.

La parte "visual" de los datos geográficos es sin duda una de sus componentes fundamentales. Creo, que alguien me corrija, que **Python no está pensado para sacar maravillosos mapas con todo lo que seo conlleva (escala, coordenadas, leyenda...)**. Pero sin duda y gracias a librerías como [Matplotlib](https://matplotlib.org/) o [Ploty](https://plot.ly/python/) podemos explotar creación de visualizaciones 2D de nuestros datos y poder crear gráficos, diagramas de dispersión, series temporales.

Para sacar el máximo partido a todo esto es interesante usar alguno de los *intérpretes interactivos con Jupyter Notebook, Anaconda, o Google Colaboratory* que descubrí preparando algunos ejemplos para la charla.

![Raster](/images/blog/202003_geopyhton/raster.png)

*Visualización de ráster con Matplotlib y histograma de bandas RGB*

## Análisis

Podemos usar diferentes librerías como GDAL o Shapely para realizar  geoprocesos de tipo  extracción, superposición, proximidad… vuelvo a comentar que en mi opinión la potencia está en generar script para realizar estas operaciones de forma recurrente según un determinado conjunto de parámetros. Para nuestra comodidad podemos usar GeoPandas una extensión de la librería Pandas de Python que  basa su funcionamiento en Shapely, Descartes y Fiona.

Hasta aquí, la verdad es que sigo prefiriendo usar un SIG para realizar mis análisis. Pero con la intención de profundizar algo más sobre este aspecto, preparando la charla encontré ejemplos para realizar análisis estadísticos más avanzados como correlaciones espaciales, detección de agrupaciones (cluster) valores atípicos con [PySAL](https://pysal.readthedocs.io/en/latest/index.html)... En este sentido creo que si es realmente interesante usar Python ya que las posibilidades son grandes y sobre todo con la posibilidad de generar salidas gráficas de representación de regresiones espaciales o análisis espacio-temporales.

![Ejemplo PySAL](/images/blog/202003_geopyhton/pysal.png)

*Ejemplo PySAL*

Otro tema que me llamó mucho la atención, que creo que supera con creces la posibilidades de cualquier SIG es todo el campo de aplicación de Pyhton en los análisis de tipo Deep learning. Gracias a la cada vez mayor generación de datos, este tipo de técnicas está siendo usado por ejemplo en el tratamiento de grande volúmenes de imágenes (aéreas, teledetección…) permitiendo realzar operaciones de clasificación ( ¿qué tipo de cobertura de superficie se observa en una imagen de satélite?), detección (detectar árboles en imágenes de drones) o segmentación (¿qué píxeles pertenecen a un edificio y cuáles no?). En este ámbito contamos con librerías como *Keras, TensorFlow o  Pytorch*.

![Deep learning](/images/blog/202003_geopyhton/depp_learning.png)

*Fuente [https://medium.com/geoai/integrating-deep-learning-with-gis-70e7c5aa9dfe](https://medium.com/geoai/integrating-deep-learning-with-gis-70e7c5aa9dfe)*

## Web

No quise terminar la charla sin al menos comentar que Python puede ser usado igualmente en el campo del desarrollo web de mapas y la programación de aplicaciones que necesiten manejar la componente especial.

Para la creación rápida de visores de mapas basados en Leaflet puede usarse [Folium](https://python-visualization.github.io/folium/) que nos permitirá cargar mapas base, añadir iconos, cargar GeoJSON o generar mapas temáticos usando Python.

![Folium](/images/blog/202003_geopyhton/folium.png)

*Mapa de coropletas con Folium*

Si lo que que queremos trabajar con datos geográficos en web de forma integrada, solo comentar que el famosos framework de desarrollo Python Django tiene una extensión que permiten almacenar y manipular datos geográficos llamada Geodjango. Gracias a [Geodjando](https://docs.djangoproject.com/en/2.2/ref/contrib/gis/) podremos trabajar con bases de datos geográficas( PostGIS, MySQL, Oracle, SpatiaLite), añadir al administrador un visor de mapas y añadir funciones geo al ORM del framework. Aunque ya hace algunos años tuve la posibilidad de montar una web con Geojango para la gestión de arbolado y mobiliario de parques y jardines y me pareció muy interesante.

![Modelo Django con atributos geográficos](/images/blog/202003_geopyhton/geodjango.png)

*Modelo Django con atributos geográficos*

<iframe src="//www.slideshare.net/slideshow/embed_code/key/kxy6NM0zO0ZHb5" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> 