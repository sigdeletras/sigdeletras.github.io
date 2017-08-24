---
title:  "Convertir archivos CAD a SIG"
excerpt_separator: "<!--more-->"
comments: true
related: true
categories: 
  - Blog
tags:
  - CAD
  - Sistemas de Información Geográfica
---

Trabajar con archivos CAD en un Sistema de Información Geográfica no es tarea fácil. Por regla general, cuando se dibuja en un programa CAD comi AutoCAD o MicroStation, no se hace pensando en incluir procedimientos que faciliten la conversión de la información espacial a un modelo de datos SIG. En esta entrada, comentaré algunas de las características estos archivos CAD que influirán en su conversión a un SIG. A continuación, y basándome en mi experiencia personal, se enumerarán los procesos básicos para intentar llevar a cabo con el mayor éxito posible este tipo de trabajo.

<!--more-->

## ¿Porqué pasar de CAD a SIG?

Podemos decir que hay dos motivos generales por las que nos vemos obligados a trabajar con datos CAD en un proyecto SIG. La primera causa es simplemente que **necesitemos usar como base una fuente de datos creados con CAD**. Suele ser frecuente que para escalas grandes, de 500 a 2000, la información cartográfica de referencia se encuentre en este formato. Quizás el caso que mejor ejemplifique este motivo es la generación de un planeamiento urbanístico. Tras los trabajos de información y ordenación, el resultado principal no deja de ser mapas temáticos (clasificaciones, calificaciones, usos, sistemas…) que usan como base CAD.

El segundo caso aborda la **generación en formato SIG de las base cartográfica unificada (plano ciudad, mapa guía, mapa base, base topográfica armonizada...) de un municipio o ciudad**. Esta información geográfica servirá de base para múltiples trabajos vinculados tanto con la generación de cartografía digital, como para la toma de decisiones sacándole el máximo rendimiento a las posibilidades metodológicas y técnicas de un sistema de información geográfico. La base será fundamental para trabajo de inventarios de infraestructuras, gestión de redes, mantenimiento callejero, estudios de geomarketing, actividades económicas y licencias, urbanismo, padrón municipal o catastro. Este mapa base servirá para la elaboración de mapas en papel  (mapas turísticos, planos de la ciudad, cartografía temática) y también para generar productos cartográficos digitales consumidos a través de servicios OGC o mapas de teselas mediante visores cartográficos.

## [![Mapa base del Visor IDE Zaragoza](https://c1.staticflickr.com/9/8491/28561488600_5528897c40_b.jpg)](https://www.flickr.com/photos/115384326@N07/28561488600/in/dateposted-public/ "virsorzaragoza")  Consideraciones sobre los datos CAD

### Formatos y versiones

Si nos centramos en SIG abiertos (gvSIG o QGIS) que suelen utilizar la librería GDAL (http://www.gdal.org/ogr_formats.html) debemos de tener en cuenta la lectura de archivos CAD se encuentra limitada a versiones menos recientes y liberadas. Por ejemplo, QGIS lee archivos DGN (http://www.gdal.org/drv_dgn.html) la versión 7/8 y lee y crea DXF en su versión 2000\. GvSIG añade la posibilidad de cargar archivos DWG.

Si necesitamos cambiar la versión de los archivos deberemos disponer los correspondientes programas propietarios o bien usar alguno libre como [Draftsight](http://www.3ds.com/es/productos-y-servicios/draftsight/) o el programa [TeighaFileConverter](https://www.opendesign.com/guestfiles/TeighaFileConverter)

### Geometrías

Los datos CAD 2D constan de primitivas geométricas. Entre los ejemplos de geometría 2D están de forma general:

*   Puntos
*   Segmentos de líneas y polilíneas cerradas que representan polígonos
*   Regiones planas 2D
*   Arcos, splines y círculos
*   Bloques

La conversión de geometrías CAD a SIG es uno de trabajos más costosos. Todo dependerá de los criterios de dibujo usados y el nivel de detalle y precisión que se haya querido dar. El proceso más recurrente será la obtención o transformación de los elementos poligonales a partir de líneas. En QGIS nos será de gran ayuda la herramienta “Poligonizar”.  

[![Poligonación en QGIS](https://c7.staticflickr.com/9/8124/28814587846_c1f298f5fa.jpg)](https://www.flickr.com/photos/115384326@N07/28814587846/in/dateposted-public/ "poligonacion") 

### Textos

La anotación en un archivo CAD se mide en unidades de mapa cuando se crea. Normalmente, el texto de una línea y multilíneas son elementos gráficos independientes que no tienen capacidad inherente para vincularse con la geometría.

Al cargarlo un SIG, los textos serán representados como un punto y el valor será almacenado en una columna de la capa. Aquí los principales problemas serán: los textos en multilínea, ya cada salto de línea será representado por un registro en la tabla, la asociación de los datos a elementos lineales como ejes de vías, estilo y simbología, codificación de caracteres.  

[![Archivo DGN en QGIS](https://c3.staticflickr.com/9/8632/28561489330_f2b2af8c41_b.jpg)](https://www.flickr.com/photos/115384326@N07/28561489330/in/dateposted-public/ "Archivo DGN en QGIS") 

### Estructura de la información

Las capas de CAD organizan los datos de manera similar a las capas de un SIG; sin embargo, no siguen el modelo de entidades simples del SIG. Los autores del CAD tienen la libertad de mezclar tipos de geometría y otros datos en una capa individual. También es posible utilizar el tipo y color de línea para clasificar mejor los datos. Como resultado, el contexto de los datos, junto con la información textual y una cantidad significativa de interpretación humana pueden ser necesarios para identificar la geometría como una entidad SIG particular.

[![Descripcion de capas de un archivo dwg. IDE Sevilla](https://c3.staticflickr.com/9/8292/28561670770_f3c6fa7815_b.jpg)](https://www.flickr.com/photos/115384326@N07/28561670770/in/dateposted-public/ "Descripcion de capas de un archivo dwg. IDE Sevilla")

Por si no fuera bastante la organización dependerá de software: AutoCAD usa el concepto capa, mientras que los archivos DGN están organizados en 63 niveles que junto a el color, estilo y peso definen cada una de las capas. Para la importación de las fuentes CAD será fundamental disponer del modelo de datos usados, en la que se defina la estructura de las capas/niveles usados y la descripción del sistema de codificación. Puede que tengamos suerte y encontremos un DWG con correcta definición de sus contenidos en la descripción de sus capas, pero también podemos encontrarnos con un listado interminable de capas definidas por códigos y si no tenemos una tabla de equivalencias será casi imposible realizar la importación. En el caso de los DGN es imprescindible.

[![Modelo de datos con la estructura de niveles DGN. IECA](https://c3.staticflickr.com/8/7651/28814722626_1741378a91_b.jpg)](https://www.flickr.com/photos/115384326@N07/28814722626/in/dateposted-public/ "Modelo de datos con la estructura de niveles DGN. IECA") 

### Georrefenciación, escalas y rotaciones

El problema de escala define una diferencia fundamental entre cómo los sistemas de SIG y CAD utilizan los sistemas de coordenadas. Un SIG modela el mundo y los objetos que contiene en una escala regional o global. Por el contrario, un sistema de CAD se utiliza para modelar los objetos reales a una escala que relativamente no se ve afectada por la superficie de la tierra. Esto conlleva que nos encontremos con datos que estén en coordenadas relativas, que no trabajemos a escala real o incluso que tengamos la información rotada.  

La mejor forma de solucionar estos problemas es hacer las correspondientes correcciones en el mismo programa CAD.

### Divisiones

Aunque esto en principio pueda no parecer un problema, es muy común encontrarnos la cartografías municipales o de planes generales divididas en hojas. A todos los trabajos anteriores habrá que añadirle la limpieza de marcos, cajas de impresión, leyendas y cartelas. Pero lo peor sin duda será el tiempo que tendremos que dedicarle a la unión de las geometrías, sobre todo las que representan áreas, que quedan en los límites entre hojas.

### Actualización

Este aspecto no tiene en principio relación con el tipo de formato CAD pero es frecuente que debido a los altos costes de los trabajos de restitución cartográfica de una ciudad no se suele contar con un cartografía CAD reciente. Esta situación deberá ser tomada en cuenta a la hora de identificar áreas transformadas y no representadas en la fecha del vuelo y la restitución. Puede sernos de gran ayuda la incorporación de las capas de Catastro y las ortofotografías existentes.

[![Comparación de archivo CAD con Catastro y PNOA](https://c6.staticflickr.com/9/8306/28231314053_d87c304074_b.jpg)](https://www.flickr.com/photos/115384326@N07/28231314053/in/dateposted-public/ "Comparación de archivo CAD con Catastro y PNOA") 

## Metodología

Dentro de los trabajos de transformación de fuentes de datos CAD a un Sistema de Información Geográfica debemos distinguir entre el conjunto de procesos a realizar con una herramienta CAD y aquellos que usaremos una vez convertida la información a SIG. Para cada uno estos procesos utilizaremos una o varias herramientas de nuestros paquetes informáticos, cuyo nombre dependerá del CAD o SIG que usemos. Por ello sólo hemos descrito el tipo de tarea a utilizar y no la herramienta usada.

### Trabajos en CAD

*   Si fuera necesario, escalado, rotación y georreferenciación de los archivos.
*   Análisis y reestructuración de capas/niveles. Limpieza de capas. Identificación textos  y generación de capas específicas de información textual.
*   Depuración de elementos de cartelas y marcos.
*   Unión de archivos (hojas), y corrección de geometrías en los bordes.
*   Mejora de la base de información, a partir de procesos de limpieza y corrección de la  
    geometría según las necesidades de los programas SIG: unión de líneas, solape de líneas, cierre de polígonos, conexión de redes, regeneración de polígonos (contornos), edición de anotaciones.
*   Conversiones de formato/versión.

### Trabajos en SIG

*   Definición de capas y modelos de datos según el análisis de archivos CAD
*   Conversión SIG (Shape, PostGIS o Spatialite) por capas/niveles.
*   Descripción de la codificación de capas/niveles.
*   Depuración entidades, corrección de errores geométricos y topológicos.
*   Transformación de líneas a polígonos de capas que lo requieran.
*   Generación de atributos de capa y estandarización de la información. Creación de tablas de dominios.
*   Asignación por localización (punto-polígono) de información de CAD en formato texto.
*   Definición de estilos, simbología y etiquetados.
*   Identificación de áreas con información desactualizada (ortofotografía, catastro...)
*   Informe de metadatos.
        
