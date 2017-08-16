---
title:  "Extrayendo datos del DERA con Python"
categories:
- blog
tags:
- Python
- Andalucia
- GDAL
- IECA
---

Los **Datos Espaciales de Referencia de Andalucía para escalas intermedias -DERA-** "_es un repertorio de bases cartográficas de diferente naturaleza geométrica (puntos, líneas, polígonos, imágenes raster) referidas al territorio andaluz_". Más información en esta página del [Instituto de Estadística y Cartografía de Andalucía](http://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/).

Los datos pueden descargarse en un archivo comprimido zip por cada uno de los bloques. Dentro de cada zip la información se encuentra accesibles por capas en formato shapefile (.shp), en sistema de referencia geodésico ETRS89 y proyectadas en UTM huso 30.

### Filtrado de datos con SIG

La extensión espacial de las capas es el ámbito geográfico de la comunidad autónoma de Andalucía. Esto significa que por ejemplo en la capa _sv01_sanidad_centro_salud.shp_ se encuentran todos los centros de salud existentes en Andalucía y sus diferentes tipologías. Si queremos trabajar con una selección de datos, por ejemplo por provincia, deberemos:

*   Descarga el zip correspondiente desde la web del [IECA](http://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/)
*   Descomprimirlo el zip
*   Abrir un Sistema de Información Geográfica (ArcGIS, QGIS, gvSIG...)
*   Cargar la capa (ej. _sv01_sanidad_centro_salud.shp_)

Normalmente las capa del DERA incluyen información del municipio y provincia, por lo que podemos hacer una consulta por el atributo que deseemos, seleccionar los datos y crear una nueva capa a partir de la selección.

Una vez que tenemos los datos en nuestro SIG, se nos pueden plantear algunas preguntas:

*   **¿Qué ocurre si la capa no dispone de un atributo como municipio o provincia que permita filtrarla?** Esto puede suceder para capas de tipo lineal o poligonal cuya extensión supere un límite administrativo.
*   **¿Cómo extraer información de ámbitos geográficos definidos por nosotros?** Este puede ser el caso de un barrio, o la delimitación de una mancomunidad. En este caso debemos contar con la capa de delimitación y a continuación seleccionar los elementos geométricos (ej. centros de salud) mediante una consulta espacial (superposición, dentro de, toca...).
*   **¿Y si quiero obtener todos los datos de un bloque temático, como por ejemplo "Servicios", para un barrio?** En este caso, tendremos que repetir la operación anterior para cada una de las capas.

### Trabajando con Python y GDAL

Algunos de los problemas que he planteado antes pueden solucionarse con las herramientas de creación de modelos de procesado integradas en los SIG. En el siguiente enlace a [MappingGIS](http://mappinggis.com/2014/08/crear-un-modelo-de-procesado-en-qgis-el-model-builder-de-qgis/) hay una sencilla guía de cómo hacerlo en QGIS.

Como sigo con el aprendizaje de Python que comencé con [dxf2gmlcatastro](2016/dxf2gmlcatastro-script-python-para-convertir-de-dxf-a-gml-parcela-catastral) he decidido crear un pequeño código que haga lo siguiente:

*   Descomprimir un archivo zip de capas Shape, en este caso del DERA.
*   Localizar una archivo poligonal que va a ser usado para "recortar" las capas Shape del zip
*   Crear una carpeta donde almacenar las nuevas capas recortadas.
*   Generar nuevas capas recortadas en una carpeta concreta y con un sufijo (_clip).
*   Borrar la carpeta donde se ha descomprimido el zip.

Los requisitos para ejecutar el código son

*   Tener instalado Python.
*   Tener instalada la librería GDAL/OGR.

Un ejemplo
```$ python clipShapesZip.py 'G15_Patrimonio.zip' 'clip_area.shp' 'clipFolder'
```

Como nota importante comentar que si el geoproceso se aplica sobre una lineal o poligonal, la función hará su función y "recortará" las geometrías a partir del la capa indicada.

{% gist sigdeletras/8f89f36cdc1a0246aea0342357fbbf3d %}
        
