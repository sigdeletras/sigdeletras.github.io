---
title:  "Procesamiento de imágenes con la librería GDAL (2ª parte). Reproyección con gdalwarp"
header:
      teaser: "/images/header/2015-10-09-gdal2.jpg"
categories: 
      - Blog
tags:
      - GDAL
---

Este artículo continua la [entrada anterior](blog/procesamiento-de-imagenes-con-la-libreria-gdal-1-parte "GDAL 1") en la se expusieron algunos de los usos de los comandos _gdalinfo_ y _gdaltranslate_ de la librería GDAL. En el siguiente texto nos vamos a centrar en el comando _gdalwarp_. Este comando se usa para hacer reproyecciones del Sistema de Referencia de Coordenadas de una imagen georeferenciada.

### Reproyección de una imagen georeferenada con gdalwarp

El uso básico es sencillo: partimos de la base de que la imagen ya posee un SRC definido, tras el comando indicaremos el SRC de salida usando el [código EPSG](https://es.wikipedia.org/wiki/European_Petroleum_Survey_Group "EPSG") (ej. -t_srs "EPSG:4326"), el fichero a reproyectar y el nombre la imagen proyectada.

      $ gdalwarp  -t_srs "EPSG:4326"  -of GTiff img.tif img4326.tif

Las opciones de _gdalwarp_ son muchos más variadas establecer un valor sin datos (_- dstnodata_) o usar una archivo vectorial para recortar la imagen de salida (_-cutline_). Todas las opciones pueden consultarse en la siguiente dirección [http://www.gdal.org/gdalwarp.html](http://www.gdal.org/gdalwarp.html "gdalwarp")

### De ED50 a ETRS89

En España, a partir del 1 de enero de 2015  y según  el Real Decreto 1071/2007 , de 27 de julio, por el que se regula el sistema geodésico de referencia oficial en España, _"...toda la cartografía y bases de datos de información geográfica y cartográfica producida o actualizada por las Administraciones Públicas deberá compilarse y publicarse conforme a lo que se dispone en este real decreto_” o lo que es lo mismos debe estar encontrarse en el ETRS89\. Más información en esta [página del IGN](http://www.ign.es/ign/layoutIn/faqgd.do).

Para facilitar la transformación del datum ED50 a ETRS89, el Instituto Geográfico Nacional ha generado dos rejillas (Península y Baleares) en formato NTV2\. Estas rejillas pueden ser descargadas desde la [web del IGN](http://www.ign.es/ign/layoutIn/herramientas.do "Rejilas NTV2").  Las rejillas pueden añadidas  usadas en la mayoría de los SIG pero también podemos utilizarla directamente usando GDAL con el comando gdalwarp. En la web de [Mappingis](http://mappinggis.com/2015/03/como-transformar-de-ed50-a-etrs89-en-qgis-con-ntv2/) podréis encontrar un artículo de su uso en QGIS.

Si queremos trasformar con _gdalwarp_ una imagen en ED50 UTM30N (EPGS:23030) a ETRS89 (EPGS:25830), lo primero será descargar la correspondiente rejilla a nuestro ordenador. Tras el comando debemos añadir los SRC de entrada (_-s_srs_) y salida (_-t_srs_), pero en esta ocasión añadiendo los parámetros de la librería PROJ.4 e indicando la ruta de la rejilla del IGN tras la opción _nadgrids_.

Suponiendo que hemos almacenado la rejilla de la península en nuestro disco duro C: en la carpeta "rejillas", el comando quedaría así:

      $ gdalwarp -s_srs "+init=epsg:23030 +nadgrids=C/:rejilla/PENR2009.gsb +wktext" -t_srs "+init=epsg:25830 +nadgrids=null +wktext" -of GTiff img23030.tif img25830.tif


### Un poco de programación: procesando de múltiples imágenes con _gdalwarp_

Como he comentado al principio, todo este textazo tiene en primer lugar una función didáctica para mi. El segundo aspecto por el que merece utilizar los comando de estas librerías es el hecho de poder crear nuestros propios fragmentos de código o _scripts_ que nos ayuden a mejorar nuestra vida..al menos desde el punto de vista informático. Creo que en esta búsqueda de la felicidad, podría ser interesante hacer un un pequeño _script_ que por ejemplo convirtiera a formato GeoTiff y mejorara el tamaño de, ¿porqué no?, 200 ficheros.

Creamos un _script_ utilizando el _shell_ de Linux con la extensión _sh_ (ej. ed50etrs89.sh). El _script_ está pensado para ser utilizado desde el terminal de Linux. Si alguno se lo trabaja para Windows o Mac, y quiere que lo ponga en la entrada avisad por correo.

El código hace lo siguiente:

*   Localiza las imágenes con la extensión JPG que se encuentran en el mismo directorio del archivo  ed50etrs89.sh
*   Reproyecta  y comprime las imágenes a ETRS89 UTM 30N usando la rejilla del IGN localizada en en mismo directorio del _script_.
*   Salva las imágenes con el sufijo “_25830”  y en formato GeoTiff
*   Usa gdalinfo para generar una archivo de texto con los metadatos de las imágenes reproyectadas.

Si es necesario le asignamos, los correspondientes permisos de ejecución con chmod

      $ chmod +x ed50etrs89.sh

Y a continuación, lo ejecutamos

      $ ./ed50etrs89.sh
        
