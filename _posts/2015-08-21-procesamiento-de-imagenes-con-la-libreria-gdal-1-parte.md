---
title:  "Procesamiento de imágenes con la librería GDAL (1ª parte)"
excerpt_separator: "<!--more-->"
comments: true
header:
      teaser: "/images/header/2015-07-07-gdal.jpg"
related: true
categories: 
- 2015
tags:
- GDAL
---
        
**GDAL** ([http://www.gdal.org/](http://www.sigdeletras.com/)) es una biblioteca de software para la lectura y escritura de formatos de datos geoespaciales publicada bajo la MIT License por la Fundación [OSGeo](%20http:/www.osgeo.org/ "OSGeo"). Con esta librería se pueden realizar multitud de operaciones de transformación y procesamiento sobre gran variedad de datos [raster](http://www.gdal.org/formats_list.html "Raster") y [vectoriales](http://www.gdal.org/ogr_formats.html "Formatos vectoriales").
<!--more-->

En la siguiente serie de entradas vamos a tratar algunos los comandos destinados a obtener información de un raster (gdalinfo), convertir archivos a otros formatos (gdal_translade) y cambiar el sistema de referencia de coordenadas  de imágenes referencias  (gdalwarp).  

Para saber más sobre esta librería se pueden consultar los siguientes artículos.

*   [Guía de inicio rápido GDAL/OGR](http://live.osgeo.org/es/quickstart/gdal_quickstart.html "enlace")
*   [Raster Processing Tutorial](https://trac.osgeo.org/gdal/wiki/UserDocs/RasterProcTutorial%20 "Raster Processing Tutorial")
*   [Workshop GDAL FOSS4GE 2015](http://download.osgeo.org/gdal/workshop "WorkshopGDAl FOSS4GE")

### ¿Terminal o SIG?

La librería GDAL es utilizada por gran número de paquetes geomáticos (https://trac.osgeo.org/gdal/wiki/SoftwareUsingGdal) como por ejemplo QGIS, gvSIG o ESRI ArcGIS 9.2+. Desde los menús de cualquiera de estos clientes SIG podemos acceder a las funciones de GDAL utilizando los formularios diseñados para ello. **Si podemos utilizar sin complicaciones las funciones desde un Sistema de Información Geográfica ¿qué sentido tiene utilizar los comandos?**. Para mi, la primera razón es el simple hecho de conocer, aprender y saber a manejar distintas herramientas vinculadas con la información geográfica. El segundo motivo, y no por ello el menos interesante, funcional y divertido es el intentar dar soluciones más efectivas mediante programación a operaciones que se repitan o en las que estén incluidas multitud de ficheros.

### Instalación de GDAL

Comenzamos con la instalación de la librería. En mi, en un equipo con **Ubuntu** he añadido repositorio de fuentes, actualizado e instalado a librería usando los siguientes comandos.

	$ sudo add-apt-repository ppa:ubuntugis/ubuntugis-unstable  
	$ sudo apt-get update  
	$ sudo apt-get install gdal-bin

Una vez instalado podremos hacer una verificación mediante este comando.

	$ gdalinfo --version

Para equipos con **Windows** lo más recomendable es utilizar el [instalador OSGeo4W](https://trac.osgeo.org/osgeo4w/ "Osgeo4w"), aunque también está la alternativa de [FWTools](http://fwtools.maptools.org/ "fwtools").

Como no me quiero meter en follones con la instalación en **Mac** por no haberla probado, aquí un dejo un [enlace](https://www.mapbox.com/tilemill/docs/guides/gdal "Instlación GDAL en Mac") que puede ayudar.

### Usando _gdalinfo_  para obtener información sobre un archivo

Podemos utilizar el comando gdalinfo para obtener gran cantidad de información de un determinado fichero de imagen. Si queremos podemos también comprobar los tipos de formatos soportados por GDAL con el comando _gdalinfo –formats_.

Si nos encontramos en el directorio donde se encuentra el archivo, desde Linux sólo debemos abrir nuestro terminal, escribir el comando seguido del nombre y extensión del fichero. En el caso de estar en otro directorio debemos añadir la ruta y el nombre más extensión del raster.

	$ gdalinfo mapa.tif

o

	$ gdalinfo utm.tif /home/user/mapa.tif

Entre otros datos obtendremos: tipo del fichero, tamaño, SRC, tamaño del píxel, metadatos, coordenadas de las esquinas y centro o la información de las bandas.

Si volvemos a escribir el comando, pero esta vez seguido del símbolo mayor que (>) con un nombre y la extensión txt (ej. utm_metados.txt), se genera un fichero con los datos. Esta opción es bastante interesante si queremos incorporar un fichero adjunto de metadatos a nuestra imagen.

	$ gdalinfo mapa.tif > mapa_metados.txt

### Cambios de formato con _gdal_translate_

La utilidad básica de [_gdal_translate_](http://www.gdal.org/gdal_translate.html "gdal_translate") es la de hacer una copia de un fichero existente en otro formato de los reconocidos por la librería.

Por ejemplo, al georreferenciar una imagen que sólo requiera escalado y traslación, lo normal es que se generar un archivo  de tipo _world file_ con los datos del píxel y la coordenada de la esquina. Estos ficheros se sombran de igual manera que la imagen y tienen una extensión acabada en la letra w. (pnw, .jpgw/.jpegw o .wld). Si utilizamos este sistema de multiarchivo la información geográfica no es intrínseca al archivo, por lo que no podremos saber el Sistema de Referencia de coordenadas en que se encuentra la imagen. Para solventar este escollo es preferible trabajar con archivos en formato GeoTiff.

Para convertir el archivo a formato GeoTiff usamos gdal_translate y añadimos el fichero de origen y el nombre del nuevo fichero con su extensión.

	$ gdal_translate -of GTiff mapa.jpg mapa.tif

Una vez realiza la conversión es interesante comprobar la diferencia de datos vinculados al fichero usando de nuevo el comando _gdalinfo_.

Lo normal es que utilicemos la librería GDAL con imágenes georreferenciados, pero puede ser también útil para pasar de formato otros archivos sin coordenadas previas. Por ejemplo, podemos convertir un plano en PDF a un archivo TIF, establecer la resolución de la imagen de salida o incluso obtener una zona concreta del PDF usando  _-projwin_.

	$ gdal_translate in.pdf out300.tif  --config GDAL_PDF_DPI 300 -projwin 792 144 9450 5600

Después utilizando un SIG o la misma librería podríamos asignarles las coordenadas para su georreferenciación.

### Opciones de compresión

Podemos ir más allá usando los distintas opciones del comando. y por ejemplo definir las opciones de configuración para aplicar compresión a fichero y reducir su tamaño. Usando el comando y la opción “-co” se podrá asignar al nuevo fichero un algoritmo de compresión que puede reducir el peso del nuevo.

	$ gdal_translate -of GTiff -co COMPRESS=DEFLATE -co PREDICTOR=2 -co TILED=YES  mapa.jpg mapa.tif

No voy a entrar en las diferentes algoritmos de compresión de imágenes que podemos utilizar pero sí os dejo unos enlaces que son de gran interés. Sólo indicar que existen opciones que nos permiten reducir casi a un 50% el peso de un fichero sin perder calidad en la imagen.

*   [GDAL: efficiency of various compression algorithms. Rudi Thiede & filed under QGIS.](http://linfiniti.com/2011/05/gdal-efficiency-of-various-compression-algorithms/)
*   [GeoTiff Compression for Dummies. Thursday, February 19, 2015\. Paul Ramsey](http://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html)
*   [GeoTiff compression benchmarking en Fernerkundung.](http://fernerkundung.github.io/GeoTiff-compression-benchmarking/)
*   [GeoTiff compression comparasion por  Kersten Clauss  en Digital Geography](http://www.digital-geography.com/geotiff-compression-comparison)
