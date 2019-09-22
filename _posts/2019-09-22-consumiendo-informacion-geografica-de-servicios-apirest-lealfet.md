---
title:  "Consumiento información geográfica de servicios API REST. Visor de mapas con Leaflet"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201909_apirest/4partelealfet/portada_4.png" 
categories: 
  - 2019
tags:
  - API Rest
  - Node
  - Express
  - Leaflet
  - webmapping
---

Este texto forma parte de una serie de [entradas vinculadas con la puesta en marcha de un servidor de tipo Rest de información geoposicionada](http://www.sigdeletras.com/2019/apirest-de-datos-geograficos-con-node-y-express/). Esta guía sería la continuación de la página titulada [Consumiento información geográfica de servicios API REST. QGIS](http://www.sigdeletras.com/2019/consumiendo-informacion-geografica-de-servicios-apirest-qgis/) donde vemos cómo acceder a nuestros datos desde Sistema de Información Geográfica QGIS.

En esta ocasión vamos a explicar **cómo crear una página web para presentar datos espaciales consumidos desde una API Rest usando la librería Javascript Leaflet**.

![html](/images/blog/201909_apirest/4parteleaflet/portada_4.png)

# Crear estructura HTML básica del proyecto

Para desarrollar esta guía es recomendable usar un editor de código tipo Sublime Text, Atom, Visual Studio Code.

Empezamos creando una carpeta en nuestro equipo que podemos llamar *appgeoservicios*. Dentro crearemos el archivo *index.html*. Si manejamos Visual Studio Code podemos usar algunos de los atajos o *snippets* para crear el código básico de una página HTML5. 

![html](/images/blog/201909_apirest/4parteleaflet/00_html.gif)

El código inicial sería el siguiente.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Visor Servicios Andalucía</title>

</head>

<body>

</body>

</html>

```

Vamos a añadir un elemento *div* dentro de la sección *body* del HTML. Una vez creado le asignaremos su identificador único (*id='map'*). Esta será la capa donde se pintará nuestro mapa. El mapa va a ocupar toda el espacio de la página por lo que definimos sus propiedades mediante CSS.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Visor Servicios Andalucía</title>

    <!-- CSS -->
    <style>
        body {
            margin: 0;
            padding: 0;
        }
        #map {
            position: absolute;
            top: 0;
            bottom: 0;
            width: 100%;
        }
    </style>

</head>

<body>
    <!-- Map container -->
    <div id='map'></div>

</body>

</html>
```

# Añadiendo librerías JS Leaflet y JQuery a nuestra página.

Existen varias librerías JavaScript que permite crear aplicaciones de mapas. Entre las las más conocidas está [Google Maps API](https://cloud.google.com/maps-platform/?hl=es), [OpenLayer](https://openlayers.org/) o [Leaflet](https://leafletjs.com/). Usaremos Leaflet para este ejemplo.

Lo primero que debemos hacer es añadir los recursos necesarios para manejar esta librería de mapas.Hay varias formas de hacer esto, pero en esta ocasión, vamos a enlazar los recursos necesarios de forma externa desde  un CDN (Content Delivery Network o Red de entrega de contenidos). Esto requiere que tengamos conexión a Internet para poder usarlos. Si desemamos tener una copia de la librería en nuestro proyecto podemos [descargar la librería de Leaflet](https://leafletjs.com/download.html) y guardarla en una carpeta de recursos dentro de nuestro proyecto.

En la sección *head*  enlazamos el archivo CSS de Leaflet. También añadimos la librería Leaflet y la biblioteca JQuery. La biblioteca [JQuery](https://jquery.com/) está pensada para ayudarnos a programar en Javascript, simplificando las llamadas a elementos del DOM, eventos, interacciones. En esta primera parte acceder la usaremos para acceder a los datos GeoJSON de nuestra API. La versión de JQuery debe ser la completa, ya la versión slim no tiene algunos recursos que necesitaremos.

```html
...

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css" />

<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
<script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"></script>

...
```

# Código Javascript del mapa

Ya que tenemos disponibles nuestros recursos, vamos a añadir el código Javascript básico para pintar nuestra capa. Por ahora metemos el código dentro de nuestra sección *body* tras la capa *map* y dentro de la etiqueta *script*. 

Necesitamos crear una variable que almacenará la instancia del objeto [L.map](https://leafletjs.com/reference-1.5.0.html#map-factory) de Lealfet y que será pintada en nuestra elemento HTML *map*. Le añadimos el método *setView* para indicarle el punto central del mapa y la escala. El par de coordenadas corresponde con el centro aproximado de Andalucía.

```javascript
// Map  objects
let map = L.map('map').setView([37.427,-4.406], 8);
```

Como mapa base usamos OpenStreetMap usando el objeto del tipo [*L.tileLayer*](https://leafletjs.com/reference-1.5.0.html#tilelayer)

```javascript
// Base map layer
let osmLayer = L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap<\/a> contributors'
}).addTo(map);
```
Ya podemos visualizar nuestra página con el mapa base en el navegador. Lo localizamos dentro de nuestro equipo y hacemos doble clic para que se abra con el navegador que tengamos por defecto. Si estamos usando Visual Studio Code podemos instalar la extensión [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) y abrir el archivo html.

![Primera versión](/images/blog/201909_apirest/4parteleaflet/01_osm.png)

El siguiente paso es incorporar una de las capas que nos suministra nuestra API Rest creada con Node.js y Express. El código puede servir añadir datos de cualquier otra API o incluso de un geojson almacenado localmente.

- Creamos una variable que almacenará un objeto del tipo [L.geoJson](https://leafletjs.com/reference-1.5.0.html#geojson). 
- En la siguiente línea usaremos la función *getJSON* de JQuery que obteniende datos en formato JSON de una determinada ubicación. Gracias a JQuery simplificamos el código que realizaría una petición usando Ajax. Dentro de los parámetros, indicamos la URL de nuestro servicio que corresponde con la solicitud GET que nos devuelve los datos de los [alojamientos de Andalucía](https://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/) según los datos del Instituto de Estadística y Cartografía de Andalucía (España). El resultado será una función que nos devulve los datos que añadiremos a nuestro objeto *L.geoJson* mendiante el método *addData*.
- Por último, debemos añadir nuestra capa vectorial al mapa con el método *addTo()*.

```javascript
// GeoJSON from API Rest
let layer = L.geoJson(null, {});

$.getJSON("http://localhost:3000/api/layers/alojamiento",  function (data)  {
    layer.addData(data);
});

layer.addTo(map);
```
Vemos el resultado en el navegador.

![GeoJSON](/images/blog/201909_apirest/4parteleaflet/02_geojson.png)

# Mostrando atributos

Ya que tenemos los datos añadidos a nuestro mapa, podemos incluir un fragmento de código que nos permita consultar los datos de la capa haciendo clic sobre ellos.

- Creamos una función que recogerá los datos (feature) de la capa (layer) y generará un *popup* con los atributos que se especifiquen usando el método *bindPopup()*. 
- Vamos a añadir un par de atributos de la capa: nombre y tipo de alojamiento. Los usaremos dentro de marcadores HTML y añadiendo algo de estilo mediante CSS.

```javascript

// Shown popup with info
function popup(feature, layer) {
    layer.bindPopup(`<div>
                        <p style="text-align:right; font-style: italic;">
                            ${feature.properties.tipo}
                        </p>
                        <h3>${feature.properties.nombre}</h3>
                    </div>`);
};
```
- Necesitamos llamar a la nueva función y asociarla a la capa. Añadimos la llamada mediante la función [*onEachFeature*](https://leafletjs.com/reference-1.3.4.html#geojson-oneachfeature)

```javascript
// // GeoJSON from API Rest
let layer = L.geoJson(null, {
    onEachFeature: popup
});
```
Vemos el resultado.

![GeoJSON](/images/blog/201909_apirest/4parteleaflet/03_popup.png)

# Organizando nuestro código.

Por ahora no tenemos muchas líneas de código en el archivo HTML. Pero si deseáramos seguir añadiendo funcionalidades a nuestra aplicación, sería recomendable fragmentar nuestro código  (ej. HTML, Javasctip, CSS) facilitando con ello su comprensión  y mantenimiento.  Para ellos vamos a generar dos nuevos archivos. 

El primer archivo se llamará *main.css* y va a contener el código que se encuentra dentro de las etiquetas *style*. Una vez creado el archivo y añadido el código, añadiremos la llamada al archivo CSS en nuestro HTML y borramos los mardadores *style*.

Vamos a realizar un proceso parecido pero con el código Javascript. Creamos un archivo *main.js*, cortamos el código que se encontraba dentro de *script* y lo pegaremos en nuestro en el nuevo archivo. Igualmente tendremos que indicar la referencia al nuevo archivo en el HTML. Para una mejora en la carga, vamos a pasar las referencias de las librerías JQuery y Leaflet justo antes del cierre de *body*. Tras ellas añadimos el enlace al nuevo archivo *main.js*.

Este será el resultado final de *index.html*

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Visor Servicios Andalucía</title>

    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css" />
    <link rel="stylesheet" href="main.css" />

</head>

<body>
    <div id='map'></div>

    <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
    <script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"></script>
    <script src="main.js"></script>

</body>

</html>
```

El archivo *main.js* quedará así
```javascript
'use strict"'

// Map  objects
let map = L.map('map').setView([37.427, -4.406], 8);

// Base map layer
let osmLayer = L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap<\/a> contributors'
}).addTo(map);

// Shown popup with info
let popup  = (feature, layer) => {
    layer.bindPopup(`<div>
                        <p style="text-align:right; font-style: italic;">
                            ${feature.properties.tipo}
                        </p>
                        <h3>${feature.properties.nombre}</h3>
                    </div>`);
};

// GeoJSON from API Rest
let layer = L.geoJson(null, {
    onEachFeature: popup
});

$.getJSON("http://localhost:3000/api/layers/alojamiento", (data) => {
    layer.addData(data);
});

layer.addTo(map);
```

Y nuestro main.css es el siguiente

```css
body {
    margin: 0;
    padding: 0;
}

#map {
    position: absolute;
    top: 0;
    bottom: 0;
    width: 100%;
}

```
Hemos añadido una barra de navegación y algo de estilo con Bootstrap. Os dejo esta animación con la aplicación funcionando.

![Bootstrap](/images/blog/201909_apirest/4parteleaflet/04_bootstrap.gif)

