---
title:  "Editores de información geográfica en Internet"
excerpt_separator: "<!--more-->"
related: true
categories:
- Blog
tags:
- Webmapping
---
     
Cada vez son más los profesionales que interesados en la publicación de sus datos geográficos en Internet se acercan por primera vez al mundo de las Tecnologías de la Información Geográfica. Durante las charlas, los talleres o por correo me suelen pedir que les recomiende alguna herramienta para empezar a generar sus datos, normalmente pensando que una vez creados, estos puedan ser accesibles en Internet.
<!--more-->
Pienso que una buena manera de comenzar es utilizar algunas de las herramientas y/o servicios para la creación de datos geográficos que nos ofrece la Red. Si las necesidades de edición, análisis y publicación de datos se hacen cada vez más exigentes siempre tendremos la oportunidad de dar el salto los Sistemas de Información Geográfica de escritorio como [QGIS](http://www.qgis.org/es/site/ "QGIS") o [gvSIG](http://www.gvsig.com/es/productos/gvsig-desktop/descargas "gvSIG"), o empezar a hacer pinitos con las librerías de mapas en web como [Leaflet](http://leafletjs.com/ "http://leafletjs.com/") u [OpenLayers](http://openlayers.org/ "http://openlayers.org/").

# Geojson.io

[Geojson.io](http://geojson.io/#map=2/20.0/0.0) se describe a sí mismo como una herramienta rápida y simple para crear, visualizar y compartir mapas. Suelo utilizarla con bastante asiduidad para generar datos espaciales de forma rápida, añadirles atributos, guardarlos en formato GeoJSON para incluirlos en visores de mapas web. Aunque parece sencilla en apariencia, tiene gran cantidad de herramientas y soporta formatos geográficos como GeoJSON, KML, GPX, CSV o TopoJSON. Podemos trabajar de forma anónima o usar nuestra cuenta GitHub y trabajar con la información de nuestros repositorios.

<iframe style="border: 1px solid black;" src="http://bl.ocks.org/d/269a7dd4cf989631ffd9" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" width="100%" height="350"></iframe>

*Visor geojson.io*

# *My Maps* de  Google

Si tenemos una cuenta Gmail podemos acceder a [My Maps](https://www.google.com/maps/d/?hl=es "My Map Google")  o lo que era hace poco GoogleMap Engine Lite, para generar mapas sobre el callejero, la imagen satélite o cualquier estilo basado en Google Map. _My Map_ está totalmente vinculado con Google Drive, por lo que podemos trabajar con archivos CSV, XLSX o KML almacenados en nuestra cuenta y diseñar nuestro mapa a partir de los mismos. Si nos sentimos cómodos trabajando con Google Drive podemos probar [Fusion Tables](https://support.google.com/fusiontables/answer/2571232).

![www.gislounge.com](http://www.gislounge.com/wp-content/uploads/2013/03/google-engine-lite.png)

*Ejemplo de mapa creado con Google My Map Engine en www.gislounge.com*

# uMap

[uMap](http://umap.openstreetmap.fr/es/) es una herramienta de código abierto que puede servir de alternativa a _My Map_ de Google. La gran diferencia es que nuestros datos se localizarán sobre mapas basados OpenStreetMap, pero por lo demás las funcionalidades son numerosas. uMap nos permite, al igual que geojson.io trabajar con gran variedad de formatos geográficos, a los que se suma los datos de [OpenStreetMap](http://www.openstreetmap.org/ "OpenStreetMap") , vincular nuestros mapas a nuestra cuentas cuentas de GitHub, OpenStreetMap, Twitter o Bitbucket o incluir los mapas en nuestra web. Un aspecto que me interesa es gran variedad de opciones relativas a simbología y usos de CSS, la opción de trabajar con múltiples capas, las presentaciones de mapas estilo diapositivas...


![Mapa con la localización de los centros vecinales de Almería con Umap](/images/blog/201507_editores/umap.PNG)

*Mapa con la localización de los centros vecinales de Almería. [Ver pantalla completa](http://umap.openstreetmap.fr/es/map/centros-vecinales-almeria_39435)*

# Carto

[Carto](https://carto.com/ "Carto") es un servicio de mapas en la nube de fácil manejo para el usuario principiante. De forma sencilla podemos ir generando nuestros propios datos o partir de datos ya creados que podremos importar desde nuestro equipo, Google Drive o Dropbox. La información podrán ser manejada en formato tabla o editada desde el mapa. Mediante su asistente se puede generar con rapidez mapas temáticos, de intensidad o “calor”, agrupados o dinámicos utilizando el estilo Torque. La información asociada a cada geometría puede ser consultada mediante ventanas emergentes que se diseñan usando alguna de las plantillas disponibles.

Pero si ya tenemos algunos conocimientos, Carto nos permite igualmente hacer consultas complejas gracias a que los datos se almacenan en una base de datos geográfica PostGIS, crear nuestra propia simbología usando CartoCSS, acceder, consultar y actualizar la información mediante su API o diseñar nuestros propios mapa usando la librería Javascript Carto.js.

<div style="text-align: center;"><iframe src="https://sigdeletras.carto.com/viz/336c862e-f309-11e4-a1c8-0e8dde98a187/embed_map" frameborder="0" width="100%" height="500"></iframe>
</div>

*Ejemplo con Carto. Mapa del Festival de los Patios de Córdoba 2015*

Me interesa vuestra opinión ¿habéis utilizado alguno de estos servicios?, ¿qué os han parecido?, ¿recomendaríais otras herramienta?        
