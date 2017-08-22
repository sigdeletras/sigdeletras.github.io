---
title:  "Mapa del Festival de los Patios de Córdoba 2015 con CartoDB"
excerpt_separator: "<!--more-->"
header:
      teaser: "/images/header/2015-10-09-gdal2.jpg"
related: true
categories: 
- Blog
tags:
- Webmapping
- Carto
- Córdoba
- Patrimonio
---
      
Mayo es uno de los meses más importantes de Córdoba. Durante estos días tienen lugar algunos de los acontecimientos festivos más relevantes de la ciudad como las [Cruces de Mayo](http://www.spain.info/es/que-quieres/agenda/fiestas/cordoba/cruces_de_mayo.html "Cruces de Mayo") , la [Feria de Nuestra señora de la Salud](http://www.spain.info/es/que-quieres/agenda/fiestas/cordoba/feria_de_cordoba.html "Feria de Córdoba") o el Festival de los Patios. En la Fiesta de los Patios, declarada [Patrimonio Cultural Inmaterial por la UNESCO en 2012](http://www.unesco.org/culture/ich/index.php?lg=es&pg=00011&RL=00846 "UNESCO"), cordobeses y turistas pueden disfrutar de estos espacio arquitectónicos y sociales visitando los patios inscritos a concurso y cuidadosamente decorados con plantas (macetas) y otros objetos típicos para tal evento.
<!--more-->
Este año, toda la información del Festival con las fichas de cada uno los patios y muchos otros apartados ha podido ser consultada en la página web [Los Patios de Córdoba](http://patios.cordoba.es/). Revisando los contenidos, y sobre todo viendo los mapas, se me ocurrió usar la información para hacer mi propio [**mapa del Festival de los Patios de Córdoba 2015**](https://sigdeletras.cartodb.com/viz/336c862e-f309-11e4-a1c8-0e8dde98a187/public_map%20 "mapa en CartoDB") usando el servicio de mapas en nube [CartoDB](https://cartodb.com "CartoDB"). Aunque los contenidos de la web se encuentran bajo licencia-tipo Creative Commons Reconocimiento 3.0, mi intención se ha centrado en la localización de los patios y la incorporación de los datos asociados mediante de enlaces a las fichas de la propia web del Festival.

### Geolocalización

El primer paso fue **generar una tabla con el listado de los patios en formato CSV** en los que incluí el nombre, la zona, la ruta relativa de acceso a la ficha de la página web y la ruta una imagen. Una vez generado este listado, el siguiente paso fue la geocodificación de las direcciones de cada uno de los patios utilizando la herramienta “Geocode CSV” de [MMQGIS](https://plugins.qgis.org/plugins/mmqgis/ "MMQGIS") de QGIS. CartoDB posee su propia herramienta de geocodifiación pero tiene un límite de operaciones que en mi caso ya había sobrepasado hace tiempo.

![Archivo CSV](/images/blog/201507_patios/csv.png)

_Tabla de datos_

El funcionamiento de esta extensión sencillo: cargamos un archivo CSV que contenga un campo con la dirección, en nuestro caso el nombre del patio, la ciudad y el país. La aplicación nos permite geolocalizar las direcciones utilizando los servicios de Google o de OpenStreetMap. Tras revisar la precisión geográfica y ajustar la localización de algunos puntos, la capa puntual con los 48 puntos fue convertida a formato GeoJSON y subida a CartoDB.

![Web Service Geocode](/images/blog/201507_patios/Web Service Geocode_356.png)

_Configuración de la herramienta de Geocoding de MMQGIS_

Los datos geográficos pueden **descargarse en distintos formatos** (CSV, SHP, KML, SVG, GEOJSON) desde e enlace al conjunto de datos o _dataset_ en cartoDB desde este [enlace](https://sigdeletras.cartodb.com/tables/festival_patios_cordoba_2015/public "dataset patios cartodb"). También es posible **hacer una llamada a la API SQL** de CartoDB desde ese mismo enlace.

### Capas auxiliares

Una de las cosas que eché en falta en los mapas de la página web oficial fue la incorporación de datos turísticos. Esta información puede servir a los visitantes a completar el recorrido por la ciudad visitando cada uno de los patios. Por esta razón decidí incorporar a CartoDB una **capa puntual denominada “turismo_cordoba”** con localizaciones turísticas tipo monumentos, museos u oficinas de turismo. Estas datos forman parte de una capa propia procedente de varias fuentes oficiales como la Junta de Andalucía o el propio Ayuntamiento.

Gracias los comentarios de [Alejandro Alameda](https://twitter.com/AlxAlameda "Twitter"), vi interesante aportar la localización de las "**fuentes de agua"** Los datos de la capa proceden de OpenStreetMap y para obtenerlos utilicé la herramienta [OverPass Turbo](http://overpass-turbo.eu/ "OverPass") . Aunque faltan muchas fuentes, hay que destacar OpenStreetMap es la única base de datos geográfica donde podemos encontrar este tipo de información. Si os interesa completar los datos de vuestra ciudad echarle un vistazo a la iniciativa [“Añade una fuente” de OpenStreetMap España](http://www.openstreetmap.es/2014/07/03/anade-una-fuente/ "OSM España").

### Simbología

Una vez cargadas las tres capas y completados sus metadatos, el trabajo siguiente se centró en el diseño del mapa (view). CartoDB dispone de herramientas asistidas o _wizards_ que ayudan a crear una mapa interactivo estéticamente atractivo.

![Tipos de simbología usando CartoCSS](/images/blog/201507_patios/simbologia_patios.png)

_Ejemplo de simbología en CartoDB_

Para la capa de patios utilicé la **simbología _“category”_** que permite representar elementos geográficos según una columna de la tabla. Me pareció correcto “pintar” los patios según su zona lo que dio una capa puntual con siete colores, un por cada zona. A esta capa se le añadió una etiqueta (_label_) del mismo color que la zona con el nombre del patio. Para trabajos más avanzados puede ser interesante usar la pestaña CSS que permite editar el código [CartoCSS](https://www.mapbox.com/tilemill/docs/manual/carto/) de la simbología. Os dejo un ejemplo del código generado para la capa patios.

La capa "Turismo" fue representada también según el tipo de elemento diferenciando entre Patrimonio, Museo y Oficina de Turismo. En este caso la representación se realizó usando algunos de los iconos de las galerías incorporadas con CartoDB. Podemos utilizar subir nuestros propios iconos o hacer referencia a otros símbolos alojados en Internet. Para las fuentes busqué y edité con GIMP un símbolo representativo que posteriormente subía a CartoDB.

### Datos asociados

Al pinchar en cada uno de los patios se obtiene una  **ventana emergentes con información** sobre el nombre del patio y la zona en la que se encuentra. CartoDB permite elegir entre varias plantillas de _pop-ups_ entre las que se encuentra una que añade una imagen en la cabecera. Para obtener la ruta competa de la imagen cree un **campo virtual mediante SQL** denominado _imghead_ que concatenaba la dirección de la web oficial con el campo img de la capa más su extensión.

	SELECT *,'http://patios.cordoba.es/patios/'|| img ||'.jpg' as imghead FROM festival_patios_cordoba_2015

_Código SQL  para genera el campo "imghead"_

Una vez generado el nuevo campo y pinchando en la pestaña “infoview” , debemos arrastrarlo al principio del listado de campos disponibles. En segundo lugar de esta lista ponemos el campo que queramos aparezca sobre la imagen, en este caso el nombre del patio.

![](/images/blog/201507_patios/popup.png)

_Ventana de datos con plantilla de imagen en cabecera_

Para terminar de diseñar la ventana de datos, y accediendo en este caso a la **vista del código HTML** que conforma la ventana de datos, decidí añadir tres enlaces, uno por los idiomas disponibles, a la ficha de datos alojada en la web oficial. Aunque esto pueda parecer más complejo, sólo es necesario tener algunos conocimientos de HTML para sacarle más partido a esta función de CartoDB.

<pre><a href='http://patios.cordoba.es/patios/detallar/pag/{{link}}' target='_blank' title='Web Patios de Córdoba'>Español</a></pre>

_Código HTML de ejemplo para generar enlaces a la ficha del patio oficial_

###  Herramientas del visor

El visor incorpora varias herramientas que pueden ser activadas o desactivadas desde el botón “Options”. Creí interesante añadir el título y la descripción del mapa, así como las herramientas de callejero, control de capas y herramientas de zum. Para terminar, y utilizando algunas de las herramientas incorporadas en la última actualización de la añadí un par de marcos a la vista con la imagen corporativa de la UNESCO y un texto con la procedencia de los datos.

<iframe src="https://sigdeletras.cartodb.com/viz/336c862e-f309-11e4-a1c8-0e8dde98a187/embed_map" frameborder="0" width="100%" height="520"></iframe>       
