---
title:  "España Finisecular. Visor de consulta Minutas Cartográficas del IGN"
header:
      teaser: "/images/header/206-02-23-visorminutas.jpg"
categories: 
- Blog
tags:
- Webmapping
- Leaflet
- Servicios OGC
---

**España finisecular** es **un visor web de visualización del [servicio de mapas WMS  de las Minutas Cartográficas](http://www.ign.es/wms/minutas-cartograficas?request=GetCapabilities&service=WMS)** mantenido por el Instituto Geográfico Nacional e incluido en la Infraestructura de Datos Espaciales de España. Para saber más sobre este servicio se puede consultar esta [entrada en el Blog de la IDEE](http://blog-idee.blogspot.com.es/2015/09/servicio-de-mapas-de-minutas.html).

Desde este visor, accesible desde este [enlace](/visorminutas/), se acceder a la capa cartográfica continua generada a partir del recorte y la georreferenciación de los mapas manuscritos en papel conservados en el Archivo Técnico del IGN. Estos mapas, según se refleja en la página del IGN,  son el resultado de los trabajos previos a la realización del Mapa Topográfico Nacional y se realizaron principalmente entre 1870 y 1950 y fueron  dibujados a escala 1:25.000, con una precisión de obtención de la información correspondiente a escala 1:50.000.

Los datos, de gran valor para trabajos o estudios históricos sobre el territorio nacional, ofrecen información de gran interés vinculaba principalmente a la red de comunicaciones, pero también incluyen datos sobre nombres geográficos, construcciones, topónimos red hidrográfica  o cultivos entre otros.

###   
<iframe style="border: 1px solid black;" src="/visorminutas" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" width="100%" height="350"></iframe>

*[Ver mapa más grande](/visorminutas)*

### Funciones principales

#### Consulta visual de la información geográfica

Junto a la posibilidad de visualizar la información geográfica, el visor “España finisecular” permite la comparación de los mapas de las minutas con otros servicios de ortofotografías y mapas tanto reciente como antiguos. Para ello se ha incluido una barra que permite aplicar transparencia a la capa de las minutas.

Las capas disponibles en esta primera versión del Visor:

*   [Ortofotos máxima actualidad del PNOA](http:/www.ign.es/wms-inspire/pnoa-ma?request=GetCapabilities&service=WMS).
*   [Cartografía Catastral](http://ovc.catastro.meh.es/Cartografia/WMS/ServidorWMS.aspx?request=GetCapabilities&service=WMS) de la Dirección General del Catastro.
*   [Primera edición de cada hoja del Mapa Topográfico Nacional 1:50.000](http://www.ign.es/wms/primera-edicion-mtn?request=GetCapabilities&service=WMS) (MTN50).
*   [OpenStreetMap](http://www.openstreetmap.org/)
*   Sobre las minutas, también puede activarse los [límites administrativos de España](http://www.ign.es/wms-inspire/unidades-administrativas?request=GetCapabilities&service=WMS).

#### Consulta de datos

Activando la opción **“Consulta de datos de minutas”** se realiza una petición GetFeatureInfo al WMS de las minutas de la que se obtiene la la fecha de creación de la minuta entre otros datos.

![](/images/blog/04_wms.jpg)

Desde esta misma consulta, se puede acceder al **enlace de descarga de la minuta** existente en el Centro de Descargas del CNIG. Los archivos georrerenciados completan la información del servicio al permitir consultar información de interés incluida en las leyendas, cartelas y anotaciones manuscritas. Estos archivos pueden ser cargados en cualquier Sistema de Información Geográfica.

#### Buscador de nombres geográficos

Usando la extensión [Geocoder,](https://github.com/perliedman/leaflet-control-geocoder) se ha incluido una buscador que accede a la base de datos de nombres geográficos [Nominatim](http://wiki.openstreetmap.org/wiki/Nominatim).

![](/images/blog/01_loc.jpg)

#### Opciones de compartir

De desarrollo propio, se ha incluido en la barra de herramientas la opción de obtener el correspondiente código HMTL para i**ncluir el visor en otras páginas web**. También se ha añadido un botón para compartir el visor en **Twitter**.

![](/images/blog/02_measue.jpg)

#### Mediciones

Gracias a la extensión  [Leaflet.measure](https://github.com/ljagis/leaflet-measure) se ha habilitado la herramienta, en inglés, de captura de longitudes y áreas. 

![](/images/blog/03_embeber.jpg)

### Tecnología

El diseño del visor está basado en la plantilla [Bootleaf](http://bmcbride.github.io/bootleaf/) utilizando la [Bootstrap](http://getbootstrap.com/) y la librería JavaScrip de mapas [Leaflet](http://leafletjs.com/).
        
