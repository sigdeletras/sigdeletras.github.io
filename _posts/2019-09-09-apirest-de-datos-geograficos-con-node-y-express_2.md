---
title:  "API Restful de datos geográficos con Node.js y Express. 2º parte"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201909_apirest/portada.png" 
categories: 
  - 2019
tags:
  - API Rest
  - Node
  - Express
---

Como dejamos reflejado en la entrada [API REST de datos geográficos con Node.js y Express](http://www.sigdeletras.com/2019/apirest-de-datos-geograficos-con-node-y-express/), montar una API REst con Node.js y Express es relativamente sencillo. En el *post*  se desarrollaba un ejemplo para el servicio de una capa que se encontraba almacenada en una base de datos PostgreSQL, a la que se le añadido la extensión PostGIS. En esta ocasión vamos a **mejorar el ejemplo para poder consultar y acceder a cualquiera de las capas que podamos tener en nuestra base de datos y obtener un catálogo sencillo de los datos**. 

El ejercio desarrolla el código de la primera entrada. Podemos generarlo según las indicaciones o descargarnos esta [primera versión de la GeoAPI desde Github](https://github.com/sigdeletras/geoapi/releases/tag/v0.1). En el archivo de ayuda vienen los comandos para instalar el servidor usando ```npm install``` y ```node server``` para iniciarlo. Todo está pensado para un entorno de desarrollo.

## Carga de capas en PostgreSQL desde QGIS

Partimos del hecho de que tenemos disponible una base de datos PostgreSQL/PostGIS y conocemos sus credenciales de acceso. Nuestra base de datos ha crecido, y ya no cuenta solo con una tabla geográfica sino que contiene múltiples capas. Hemos añadido algunas de las capas suministradas por el **Instituto de Estadística y Cartografía de Andalucía**. En concreto, se han cargado algunas capas puntuales sobre servicios (farmacias, centos educativos, ayuntamientos, museos...) del [DERA](https://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/g12.htm).

![Capas DERA-IECA](/images/blog/201909_apirest/2parte/00_capas_dera.png)

Aunque queda fuera del objetivo de esta entrada, indicar que la importación de las capas se ha hecho usando el Sistema de Información Geográfica [QGIS](https://www.qgis.org/es/site/). Para facilitar la carga se ha diseñado un modelo que selecciona las capas SHP de un directorio, las reproyecta al sistema de referencia WGS 84, transforma los objetos de geometrías multiparte (MULTYPOINTS) a sencillas (POINT) y las almacena en nuestra base de datos local.

![Modelo QGIS](/images/blog/201909_apirest/2parte/01modeloqgis.png)

## Acceso a capas desde URL

La primera versión de la GeoAPI permitía obtener el archivo GeoJSON de una capa mediante la URI [http://localhost:3000/api/layers/layer](http://localhost:3000/api/layers/layer). 
Vamos a realizar las modificaciones correspondientes para poder obtener el fichero de cualquiera de las capas almacenadas.

- El nombre de la capa la vamos a obtener desde la URL y será almacenada en una variable usando el método **request.params** . Esta variable será usada dentro del SQL.
```javascript
let layername = request.params.layername;
```
- Hemos generalizado la sentencia SQL para que nos devuelva todos los campos. El nombre de la tabla será obtenida desde la URL.

let queryLayer = `SELECT  * FROM ${layername};`
```
- Se ha mejorado el código de respuesta para que nos devuelva JSON con un mensaje de aviso si hay error.
```javascript
    pool.query(queryLayer, (err, res) => {
        if (err) {

            console.error('Error ejecutando la consulta. ', err.stack)

            // Mensaje de aviso si no se ha encontrado al capa con el nombre indicado 
            return response.json({
                mensaje: `La capa ${layername} no existe en la base de datos`
            })
        }
```
- Al generalizar la consulta SQL, se añade también el campo *geom* con la geometría en formato WKT de cada elemento. Este dato no es necesario,  por lo que usamos un breve código usando la función *omit* del paquete [Underscore.js](https://underscorejs.org/) para eliminarlo de nuestro JSON. El paquete debe ser instalado usando ```npm install underscore -S``` y añadido a nuestro controlador.

```javascript
const _ = require('underscore');

....
        // Definimos una nueva variable donde almacenar los datos sin el valor geom.
        // Para ellos recorremos el array y usamos omit de undercore para omitirlo.
        let rowNoGeom = []; 
        res.rows.forEach(element => {
            let row = _.omit(element, 'geom'); 
            rowNoGeom.push(row);

        });

```

El código definitivo de la función *getGeojson* quedaría así.

```javascript

// controllers/layerController.js
const _ = require('underscore');

....

// Almancenamos en una constante la función que realiza la llamada y devuelve el archivo.
const getGeojson = (request, response, next) => {

    // Creamos una variable para almacenar el valor del parámetro con el nombre de la capa.
    let layername = request.params.layername;

    // Almacenamos la consulta SQL añadiendo la variable
    let queryLayer = `SELECT  *,  st_x(geom ) as lng, st_y(geom ) as lat FROM ${layername};`

    pool.query(queryLayer, (err, res) => {
        if (err) {
            
            console.error('Error ejecutando la consulta. ', err.stack)

            // Mensaje de aviso si no se ha encontrado la capa con el nombre indicado 
            return response.json({
                mensaje: `La capa ${layername} no existe en la base de datos`
            })
        }

        // Definimos una nueva variable donde almacenar los datos sin el valor geom.
        // Para ellos recorremos el array y usamos omit de undercore para omitirlo.
        let rowNoGeom = [];
        res.rows.forEach(element => {
            let row = _.omit(element, 'geom');
            rowNoGeom.push(row);

        });

        let geojson = GeoJSON.parse(rowNoGeom, { Point: ['lat', 'lng'] });

        response.json(geojson);
    })
}

```

Ahora vamos a modificar nuestro fichero de rutas **routes/api.js**. Solo debemos añadir dos puntos antes de *layername* para que este valor se convierta en un parámetro dentro de nuestra URL. Este será el valor que usará el controlador dentro de la SQL.

```javascript

// routes/api.js

// Añadimos al ruta el parámetro layername para ser usado por el controlador.
router.get('/layers/:layername', layer.getGeojson)

```

Guardamos todos los cambios y reiniciamos el servidor. Podemos usar [Postman](https://www.getpostman.com/) para probar las nuevas funcionalidades.

En este primer ejemplo vamos a obtener el GeoJSON de la capa *museo* mediante la url [http://localhost:3000/api/layers/museo](http://localhost:3000/api/layers/museo)

![Postman Museo](/images/blog/201909_apirest/2parte/02_postman_museo.png)

Ahora vamos a comprobar que nos devuelve cuando pedimos una capa que no existe (ej.hotel) [http://localhost:3000/api/layers/hotel](http://localhost:3000/api/layers/hotel)

![Postman hotel](/images/blog/201909_apirest/2parte/03_postmanhotel.png)

## Creación de un petición para catálogo de metadatos.

El volumen de nuestra información va aumentado y esto conlleva mejorar la APIRest para faciltar al usuario el uso de la misma. Una buena opción puede ser añadir un nueva función que nos informe de las capas geográficas disponibles.

Al habiliar la extensión PostGIS en nuestra base de datos se nos ha añadido una vista que registra información sobre las distintas capas geográficas almacenadas. La vista en concreto se denomina *geometry_columns* que presenta varios campos. Para nuestro ejercicio, solo vamos a querer que nos muestre el nombre de la capa, su dimensión, el sistema de referencia y el tipo de geometría.

También contamos con una tabla (*information_schema.COLUMNS*) propia de PostgreSQL con el registro de los campos de cada tabla.

Para obtener el JSON con la combinación de ambas capas usaresmos la función *json_build_object* de PostgreSQL. Tras algunas consultas en foros, esta parte del código podría sustituirse usando promesas, por lo que habrá que mirarlo con más detalle.

Volvemos al archivo de controlador y añadimos la función *getLayersMetadata*. No se nos puede olvidar añadirla también en las exportaciones.

```javascript
// controllers/layerController.js

// Función para obtener metadatos de capas
const getLayersMetadata = (request, response, next) => {

    // Generamos la consulta añadiendo la función  json_build_object para crear el JSON con las tablas geográficas y sus atributos
    let queryLayers = `SELECT json_build_object(
        'name', t.f_table_name, 
        'coord_dimension', t.coord_dimension, 
        'srid', t.srid, 
        'geom_type', t.type,
        'fields', 
            (SELECT json_agg(json_build_object('field_name', f.column_name, 'field_type', f.udt_name)) 
            FROM information_schema.COLUMNS f WHERE t.f_table_name = f.table_name
            )
        ) as layer FROM geometry_columns t`;

    pool.query(queryLayers, (err, res) => {
        if (err) {
            console.error('Error ejecutando la consulta. ', err.stack)
            return response.json({
                mensaje: `No existe capas geográficas en la base de datos`
            })
        }

        response.json(res.rows);
    })
}
// Exportamos las funciones para ser usadas dentro de la aplicación
module.exports = { 
    getGeojson,
    getLayersMetadata
} 

```

Para terminar añadimos una nueva ruta a *api.js*. 
```javascript
// URL para obtener el listado de capas de nuestra base de datos
router.get('/catalog', layer.getLayersMetadata)
```
Guardamos los cambios y reiniciamos el servidor.


Para comprobar el resultado, usamos en esta ocasión el navegador. Podemos instalar alguna de las extensiones para Chrome que mejoran el aspecto visual de los JSON. La captura siguiente está usando JSONViewer y presenta los resultados de [http://localhost:3000/api/catalog](http://localhost:3000/api/catalog)

![Postman hotel](/images/blog/201909_apirest/2parte/04_catalog.png)

El código del ejericio se encuentra disponible en [Github](https://github.com/sigdeletras/geoapi/releases/tag/v0.2).
