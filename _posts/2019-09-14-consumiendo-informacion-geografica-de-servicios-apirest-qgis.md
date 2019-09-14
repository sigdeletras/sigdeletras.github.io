---
title:  "Consumiento información geográfica de servicios API REST. QGIS"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201909_apirest/3parteqgis/portada.png" 
categories: 
  - 2019
tags:
  - API Rest
  - Node
  - Express
  - QGIS
---

Vamos a continuar con la [serie de entradas](http://www.sigdeletras.com/2019/apirest-de-datos-geograficos-con-node-y-express_2/) vinculadas con la **creación de una APIRest para ofrecer servicios y datos geográficos con Node.js y Express**. Toca describir las formas de consumir estos datos. Empezamos indicando cómo hacerlo desde un Sistema de Información Geográfica, en concreto con la última versión de [QGIS](https://www.qgis.org/es/site/), la 3.8 Zanzibar

# Añadir mapa base mediante *server tiles*
Arrancamos QGIS para añadir una capa base sobre la representar nuestros datos. Los recursos son grandes, pero para esta entrada vamos a cargar como mapa de referencia OpentreeetMap mediando servicio de teselas del tipo *XYZ Tiles*. 

- Accedemos desde el menú a **Capa>Administrador de fuentes de datos** y elegimos **Navegador**.
- Dentro de las opciones que nos presenta QGIS hacemos clic y botón derecho sobre *XYZ Tiles*. Elegimos la opción *"Conexión nueva"*.
- Damos un nombre a nuestra nueva conexión (ej. OpenStreetMap) y añadimos la URL del servicio *https://tile.openstreetmap.org/{z}/{x}/{y}.png*

![XYZ Tiles](/images/blog/201909_apirest/3parteqgis/01_xyxtiles.png)

Tras crear la conexión, añadimos como capa el servicio simplemente haciendo doble clic.

Podemos encontrar más ejemplos de [servicios de teselas de OpenStreetMap](https://wiki.openstreetmap.org/wiki/Tile_servers) en la página web del proyecto. Si lo que queremos es añadir las teselas de Google Maps estas son las URL:

- Google Maps: https://mt1.google.com/vt/lyrs=r&x={x}&y={y}&z={z}
- Google Satellite: http://www.google.cn/maps/vt?lyrs=s@189&gl=cn&x={x}&y={y}&z={z}
- Google Satellite Hybrid: https://mt1.google.com/vt/lyrs=y&x={x}&y={y}&z={z}
- Google Terrain: https://mt1.google.com/vt/lyrs=t&x={x}&y={y}&z={z}
- Google Roads: https://mt1.google.com/vt/lyrs=h&x={x}&y={y}&z={z}

# Cargando capas desde nuestra geo API

En las dos entradas anteriores dimos unas guías generales de cómo [crear una API Rest de datos geográficos con Node.js](http://www.sigdeletras.com/2019/apirest-de-datos-geograficos-con-node-y-express) y [cómo configurarla para poder obtenter GeoJSON](http://www.sigdeletras.com/2019/apirest-de-datos-geograficos-con-node-y-express_2/) de datos almacenados en PostgreSQL/PostGIS.

Trabajábamos en un entorno de desarrollo, en el que está levantado nuetro servidor REST. La API desarrollada permitía consultar el listado de capas dispobibles mediante una petición GET usando la dirección *http://localhost:3000/api/catalog*. Si queríamos obtener el archivo GeoJSON de una capa concreta (ej.centros) debíamos escribir en nuestro navegador *http://localhost:3000/api/layers/centrosalud*.

![Servisios API Rest](/images/blog/201909_apirest/3parteqgis/02_geoapi.png)

# Consumientos servicos API Rest desde QGIS

Esta misma petición HTTP es la que podemos usar en QGIS para trabajar con cualquiera de las capas servidas en nuestro proyecto geográfico. 

- Volvemos al **Administrador de fuentes de datos** de QGIS y seleccionamos la opción *Vectorial*. 
- En esta ocasión indicaremos que el tipo de fuente ser *Protocolo: HTTP(S), cloud, etc...*
- Dentro del apartado Protocolo selecionamos la opción GeoJSON
- Añadimos la URI *http://localhost:3000/api/layers/centrosalud*

![Capa en QGIS](/images/blog/201909_apirest/3parteqgis/03_protocolohttp.png)

Tras hacer clic en *Añadir*, comprobaremos que ya tenemos cargada la capa de centros de salud de Andalucía en el mapa. Podemos hacer zum a capa y consultar las propiedades.

![Capa en QGIS](/images/blog/201909_apirest/3parteqgis/04_carga_infoqgis.png)

# Complementos QGIS para consumir datos de API Rest

Tras las pasadas entradas, he tenido la oportunidad de hablar con algunos compañeros sobre el tema de servir datos geográficos mediante APIs frente a servicios [OGC de tipo WFS](https://www.opengeospatial.org/standards/wfs). Habría que sopesar el coste en desarrollo e infraestructuras según el alcance del proyecto, analizar pros/contras y un conjunto de aspectos que quedan fuera de esta entrada. 

Si tras este análisis de requisitos, llegáramos a poner en marcha un servicio con estas tecnologías basadas en Javascript, seria interesante contemplar **el desarrollo de complementos o plugins que haga más accesible el acceso a los servicios ofrecidos desde un SIG**. Esto sería una acción que mejoraría la integración de la API y el consumo de sus servicios. 

En una búsqueda rápida del término "API" en el catálogo de complementos de QGIS he encontrado un par de ellos de ejemplo con datos comunidades o ciudades españolas.

- Para Canarias se puede usar el complemento de QGIS de acceso a los datos suministrados por el [Instituto Canario de Estadística (ISTAC)](https://plugins.qgis.org/plugins/author/Instituto%20Canario%20de%20Estad%C3%ADstica%20(ISTAC)/).

![Canarias](/images/blog/201909_apirest/3parteqgis/05_isteca.png)

- Existe también el complemento [GeoBarcelona](https://plugins.qgis.org/plugins/geobarcelona/) que "*permite buscar y hacer zoom a cualquier dirección de la ciudad de Barcelona, utilizando el servicio web RESTful "GeoBcn" (https://w33.bcn.cat/GeoBcn) proporcionado por el Ayuntamiento de Barcelona.*" 

![Barcelona](/images/blog/201909_apirest/3parteqgis/06_geobarcelona.png)

Creo que son un par de ejemplos de interés que pueden apoyar la idea de montar este tipo de servicios al menos con datos públicos. Desde el punto de vista empresarial los beneficios son igualmente enormes y seguro que existen un número grande de desarrollos pero al ser propios son desconocidos.