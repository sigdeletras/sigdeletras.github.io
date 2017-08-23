---
title:  "Datos geográficos para la provincia de Almería"
excerpt_separator: "<!--more-->"
related: true
categories:
- Presentación
tags:
- Almería
---
        
Navegando por Internet podemos apreciar que la visualización o presentación de información geográfica en páginas web está cada vez más presente. Hoy por hoy, no es muy complicado incluir en nuestra página un mapa con la localización de nuestro negocio o la sede de un evento. La forma más rápida es obtener dicho mapa directamente desde Google Maps, usando otras alternativas abiertas como [OpenStreetMap](http://www.openstreetmap.org/ "http://www.openstreetmap.org/"), o trabajar con alguna de las extensiones de mapas que incorpora Wordpress, Joomla o Drupal. 

Sin embargo, si queremos dar un paso más en la presentación de nuestros datos, por ejemplo mostrando un mapa de densidad o una visualización temática de una determinada variable, podemos usar servicios de mapas en nube como [CartoDB](http://cartodb.com/ "http://cartodb.com/") o [My Maps de Google](https://www.google.com/maps/d/ "https://www.google.com/maps/d/"). Para proyectos más personalizados, en las que ya es necesario tener conocimientos básicos de HTML, CSS y JavaScript podemos recurrir a librerías de mapas como [OpenLayers](http://openlayers.org/ "http://openlayers.org/") o [Leaflet](http://leafletjs.com/ "http://leafletjs.com/").

El aspecto tecnológico vinculado a la creación de un visor de mapas parece un tema bastante solucionado. Pero existe otra cuestión que hay que tener en cuenta: la relacionada con la generación de los datos geográficos a representar o incluso la obtención de bases cartográficos a los que vincular nuestra recopilación de datos como puede ser una capa vectorial con los límites de los municipios de una provincia.

Con esta finalidad, la de conocer las principales fuentes de información geográficas para el diseño de un mapa en Internet, la gente de **HackLab Almería** organizó el pasado día 12 de mayo el [Taller «Fuentes de información geográfica para la provincia de Almería»](http://hacklabalmeria.net/actividades/2015/05/12/fuentes-datos-almeria.html "http://hacklabalmeria.net/actividades/2015/05/12/fuentes-datos-almeria.html"). Durante la charla presenté una recopilación de enlaces a páginas web de la administración como el Centro Nacional de Información Geográfica del Ministerio de Fomento o el Instituto de Estadística y Cartografía de Andalucía, desde la que se puede descargar información geográfica. También incluí datos sobre el estado de los datos geográficos en distintas web municipales y de la provincia de Almería.  

[![](/images/blog/Captura.PNG)](http://sigdeletras.github.io/2015-ig-almeria/ "Enlace a la presentación")

Dentro del [repositorio de Github](https://github.com/sigdeletras/2015-ig-almeria/) donde se encuentra la presentación, he creado la [carpeta DATOS con conjuntos temáticos de datos para la provincia de Almería](https://github.com/sigdeletras/2015-ig-almeria/tree/gh-pages/datos) procedentes de los *Datos Espaciales de Referencia de Andalucía (DERA)*. Las capas están en formato [geoJSON](http://geojson.org/ "http://geojson.org/") y se encuentran convertidos al sistema de coordenadas WGS84.

_ Localización de los ayuntamientos de los municipios de Almería. Fuente DERA_

A modo de reflexión, sólo apuntar que cada vez me encuentro en este tipo de actividades con asistentes cuyos perfiles profesionales no están tradicionalmente vinculados al mundo “geo”, pero que empiezan a estar interesados en el uso de las Tecnologías de Información Geográficas. Un buen ejemplo son los profesionales que trabajan en el ámbito del Periodismo de Datos o los diseñadores gráficos. Por otro lado, una vez que se empiezan a conocer estas herramientas, por propia evolución, en estos casos se hace necesario ir adquiriendo conocimientos más concretos sobre tipos de formatos geográficos, sistema de referencia de coordenadas o incluso plantearse empezar a manejar aplicaciones como los Sistemas de Información Geográfica para generar y preparar los datos geográficos que van a ser presentados en Internet.
        