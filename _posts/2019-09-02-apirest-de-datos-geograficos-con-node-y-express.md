---
title:  "API REST de datos geográficos con Node.js y Express"
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

# ¿Para qué una API?

Si dentro de nuestro sector o negocio la geolocación de los datos (ej. alojamientos turísticos, sedes bancarias, infraestructuras lumínicas, arbolado, clientes potenciales, comercios, localización de población...) es relevante, con toda seguridad contaremos en nuestra base de datos con un espacio dedicado a almacenar esta información. 

![Etiquetastolocas](/images/blog/201909_apirest/portada.png)

La ubicación podrá ser recogida en forma de par de coordenadas (longitud/latitud, x/y) o bien mediante un  literal que describa su 'identificación' geográfica (calle/número, parcela catastral, ciudad, PK...). Este dato puede almacenarse de forma sencilla como un campo de tipo  númérico o como una  cadena de texto. Otra alternativa más avanzada es la instalación de extensiones o complementos, como PostGIS para PostgreSQL, que doten a nuestra gestor de bases de datos de funciones de análisis espacial, permitiendo con ello aumentar el valor de nuestra información. Gracias a ello, podemos  adentrarnos líneas de negocio y estrategias basadas en lo que se conoce como *[Location Intelligence](https://es.wikipedia.org/wiki/Inteligencia_de_localizaci%C3%B3n)*.

La puesta en marcha de una API, en concreto de una [API Rest](https://bbvaopen4u.com/es/actualidad/api-rest-que-es-y-cuales-son-sus-ventajas-en-el-desarrollo-de-proyectos), que establezca los mecanismos y protocolos para que otros sistemas y aplicaciones puedan consumir nuestros datos, es sin duda una magnífica idea que nuestra empresa puede contemplar. Disponer de una API puede **mejorar considerablemente nuestra propia infraestructura tecnológica**. Otra gran posibilidad es la de diseñar **nuevos canales de distribución de datos**, especialmente si son datos generados con dinero público, como es el caso de los datos geográficos de las administraciones gubernamentales. Y por último, y no menos importante, puede convertirse en una **líena comercial de nuestra empresa** y ser ofrecidos como un servicio de pago más (así rápido, me viene a la cabeza las tarifas de uso de la API de Google Maps).

El objetivo principal de este artículo es realizar una **guía básica para la puesta en marcha de una API Rest desarrollada con Node.js y Express, que permita ofrecer datos geográficos almacenados en una base de datos PostgreSQL/PostGIS**. Se espera que la entrada pueda servir para montar una API Rest básica, pero con la novedad de que los datos ofrecidos se encuentran en formato geográfico, en concreto eh GeoJSON. Estos datos podrán ser consumidos desde applicaciones de mapas en web y SIG de escritorio.

Lamentablemente no se dispondrá de una aplicación lista para producción. Faltarían temas más avazanzados de autentificación, subida producción, seguridad...Pero sí se podrá ver la facilidad de montar este tipo de servicios con Node.js y las grandes posibilidades que se nos pueden abrir con ello.

# Requisitos

Partimos de la base de que tenemos instalado Node.js y el gestor de paquetes NPM. De forma muy sencilla comentar Node.js es un entorno Javascript del lado del servidor, basado en eventos. En el caso de no disponer de Node.js puede descargarse para cualquier sistema operativo desde la [página oficial del proyecto Node](https://nodejs.org/es/). Junto a Node.js se instalará el gestor de paquetes [npm](https://es.wikipedia.org/wiki/Npm) que nos permitirá ir añadiendo los módulos necesarios para montar nuestra API Rest.

Podemos comprobar si tenemos instalado Node.js ejecutando desde consola el comando.

```
$ node -v
```

Es interesante tambińe trabajar con algún IDE o con un editor de código. Para esta guía se ha usado [Visual Studio Code](https://code.visualstudio.com/)

Para terminar, indicar que los datos espaciales estarán almacenados en una base de datos PostgreSQL a la que se ha añadido la extensión geográfica [PostGIS](https://postgis.net/). Debemos conocer la IP o host de nuestra base de datos, el puerto, el usuario y contraseña de acceso y el nombre de la base de datos geográfica. Por ejemplo, si tenemos instalado localmente Postgres el host será 127.0.0.1 y por defecto el puerto será 5432. Nuestra base de datos se va a llamar *data* a la que se le ha cargado la extensión PostGIS. Hemos añadido una capa de ejemplo, que se denomina **alojamientosdera** en coordenadas geográficas EPGS:4326 y que proviene de los [Datos Espaciales de Referencia de Andalucía](https://www.juntadeandalucia.es/institutodeestadisticaycartografia/DERA/) que suministra el IECA.

# Inicializando con **npm**

En primer lugar vamos a crear una carpeta para nuestro proyecto a la que podemos llamar */geoapi*. Situándonos dentro de la misma, y desde el terminal ejecutamos el comando *npm init*. Vamos completando si queremos los datos que nos son requeridos. Podemos dejar los que vienen por defecto, a excepción del archivo de entrada (entry point) que vamos a llamar server.js.

![Drag Racing](/images/blog/201909_apirest/01_npm_init.png)

Tras aceptar se nos habrá creado el archivo *package.json*. Este archivo será usado para indicar la dependencias  que usaremos en nuestra aplicación. Nuestro primer módulo a instlar será Express.js que nos permitirá crear aplicaciones web y API. En esta ocasión vamos a querer que el paquete se instale como dependencia del proyecto añadiendo al comando el parámetro *--save*. 

```
$ npm install express --save
```

Si abrimos el archivo *package.json* podemos ver como ha sido añadido Express.

![Drag Racing](/images/blog/201909_apirest/02_express.png)

De la misma forma instalamos dos paquetes más que vamos a usar más adelante. Los paquetes son [pg](https://www.npmjs.com/package/pg) que nos permitirá trabajar con los datos de nuestra base de datos PostgreSQL y [geojson] que usaremos para transformar la información al formato geográfico GeoJSON.

```
$ npm i --save  pg geojson
```

# Empezando con nuestra API. Archivo **server.js**.

Vamos a crear nuestro archivo principal que se llamará *server.js* dentro de la carpeta del proyecto . El archivo va a contener el siguiente código:

```javascript
//server.js

// Llamamos al módulo Express y lo asignamos a app
const express = require("express");
const app = express();

// Añadimos una respuesta para la peticición HTTP de tipo GET a la url raiz (/).
app.get('/', function (req, res) {
  res.send('Hola GeoAPI!');
});

// Se inicia la aplicación en el puerto 3000. 
app.listen(3000, () => {
 console.log("API de datos geográficos. El servidor está inicializado en el puerto 3000");
});

```
Para arrancar el servidor escribimos en consola:

```
$ node server.js
```

Podemos contemplar que nos aparece el correspondiemte mensaje en consola.

![Drag Racing](/images/blog/201909_apirest/03_node_server.png)

Si abrimos nuestro navegador y escribimos la siguiente URl http://localhost:3000/ veremos nos devuelve la página con el mensaja "Hola GeoAPI".

![Drag Racing](/images/blog/201909_apirest/04_hello.png)

Para detener el servidor, dentro de nuestro terminal pulsamos las teclas Ctrl+c. Realizaremos esta suceción de comandos cada vez que queramos actualizar nuestro servidor con la modificaciones que hagamos en  nuestros scripts. Existe otro módulo denominado [nodemom](https://www.npmjs.com/package/nodemon) de gran utilidad para recargar el código de forma automática, pero no vamos a usarlo en este ejemplo.

## Diseño de controladores de datos.

A continuación vamos a añadir el código que desarrolla la parte lógica de la aplicación y que se encarga de realizar las peticiones a la base de datos y devolvernos los datos en formato JSON. 

Para empezar, creamos un fichero que almacenará las credeciales de acceso a la base de datos. Los datos de este archivo de configuración serán posteriormente usados por el módulo **pg* para crear la conexión a la base de datos. Como indicamos al inicio, nuestra aplicación está pensada dentro de un entorno de diseño. En el caso que quisieramos ponerla en producción, deberíamos proteger las credenciales y definirlas como variables de entorno.

Creamos un nuevo archivo en la raiz que llamaremos **config.js**

```javascript
// config.js

// Creamos un objeto con los parámetros de conexión. Los datos deben corresponder con los de nuestra base de datos.
const config = {
    db: {
        host: '127.0.0.1',
        user: 'postgres',
        password: 'postgres',
        database: 'data',
        port: 5432,
    }
};

// Usamos este objeto para que el código sea accesible desde cualquier parte de nuestra aplicación
module.exports = config;
```

Vamos hora a crear el controlador de acceso a nuestra capa geográfica. Creamos una nueva carpeta que denominaremos **/controllers** y dentro de ella un nuevo archivo que llamaremos **layerController.js**. Como punto de partida configuramos la conexión a nuestra base de datos usando el módulo *pg*

```javascript
// Mediante la función require llamamos a los módulos que vamos a usar y los almacenamos en variables
const Pool = require('pg').Pool
const GeoJSON = require('geojson');

//  Recuperamos los datos de config.js y los pasamos a variables
const config = require('../config');
const { db: { user, host, database, password, port } } = config;

// Usando el objeto Pool del módulo pg  instanciamos un nuevo objeto que usará las credenciales definidas.
const pool = new Pool({
    user: user,
    host: host,
    database: database,
    password: password,
    port: port,
})
```

Ahora vanmos a definir la consulta para que nos devuelva, y pinte en consola, el JSON con los datos de la capa 'alojamientosdera'.

```javascript
// Almacenamos la consulta SQL
let queryLayer = 'SELECT  * FROM alojamientodera;'

// Callback que retorna los datos de la consulta
pool.query(queryLayer, (err, res) => {
    if (err) {
        return console.error('Error ejecutando la consulta. ', err.stack)
    }
    console.log(res.rows)
    pool.end()
})
```
Si se está ejecutando el archivo *server.js* lo detenemos. Ahora vamos a ejecutar fichero del controlador y ejecutar la consulta.

```
$ node controllers/layerController.js
```

![Drag Racing](/images/blog/201909_apirest/05_json.png)

Podemos ver en la terminal los datos devueltos, donde se presentan los atributos de la tabla. En atributo *geom* contiene la geometría de la capa, en este caso puntual, en formato WKB (Well-Known Binary). No podemos usar los datos almacenados en este formato y necesitamos obtener las coordenadas X e Y. Usamos las funciones ST_X y ST_Y de PostGIS. Cambiamos el código SQL y volvemos a ejecutar con el comando node el fichero del controlador.

```javascript
// Almacenamos la consulta SQL
let queryLayer = 'SELECT  id,  st_x(geom ) as lng, st_y(geom ) as lat, nombre,  tipo,  cod_mun,  municipio,  provincia FROM alojamientodera;'
```
Aunque hemos solucionado este primer problema, nuestro objetivo es obtener el archivo GeoJSON. Vamos a usar las funciones del módulo *geojson* que instalamos al principio. El módulo "parsea" el archivo JSON adaptándolo a la [especificación](https://geojson.org/) de los ficheros GeoJSON. Puede verse más ejemplos en la [página del módulo](https://www.npmjs.com/package/geojson). 

![Drag Racing](/images/blog/201909_apirest/06_geojson_sample.png)

El controlador debe quedar de la siguiente forma.

```javascript
// Callback que retorna los datos de la consulta
pool.query(consultaAlojamientos, (err, res) => {
    if (err) {
        return console.error('Error ejecutando la consulta. ', err.stack)
    }
    // usamos la función parse del módulo geojson para convertir el resultado en un fichero GeoJSON.

    let geojson = GeoJSON.parse(res.rows, { Point: ['lat', 'lng'] });
    
    // devolvemos los datos formateados
    console.log(geojson)
    
    pool.end()
})
```
# Generando el direcionamiento (routing) para obtener el geojson

El último paso es generar la ruta o punto final de la aplicación que responda a la solucitud GET para la obtención del GeoJSON. El primer paso es transformar la consulta en una función que será llamada cuando se requiera. Eliminamos el código anterior que realiza la consulta por el siguiente.

```javascript
// Almacenamos en una constante la función que realiza la llamada y devuelve el archivo.
const getGeojson = (request, response, next) => {
    // Almacenamos la consulta SQL
    let queryLayer = 'SELECT  id,  st_x(geom ) as lng, st_y(geom ) as lat, nombre,  tipo,  cod_mun,  municipio,  provincia FROM alojamientodera;'

    pool.query(queryLayer, (err, res) => {
        if (err) {
            return console.error('Error ejecutando la consulta. ', err.stack)
        }
        let geojson = GeoJSON.parse(res.rows, { Point: ['lat', 'lng'] });

        response.json(geojson);
    })
}

// Exportamos las funciones para ser usadas dentro de la aplicación
module.exports = { getGeojson } 

```

Ahora vamos a añadir la ruta. Pensando en la modularización de nuestro código vamos a crear una nueva carpeta en la raiz que llamaremos */routers*  y dentro de esta crearemos el archivo *api.js*. Más información en la [documentación de Express](https://expressjs.com/es/guide/routing.html)

```javascript
// api.js

// Importamos los paquetes para crear la ruta 
const express = require('express');

// La clase Router permite crear rutas modulares.
const router = express.Router();

// Importamos el archivo del controlador
const layer = require('../controllers/layerController')

// Definimos la ruta para el método GET y añadimos como middleware la función del controlador
router.get('/layers/layer', layer.getGeojson)

// Exportamos el código 
module.exports = router;

```

Como punto final debemos añadir antes de *app.listen* la nueva ruta a nuestro fichero principal *server.js*. Hemos apañado en la URL la palabra /api para una mejor organización.

```javascript
// Importamos el archivo de rutas
const layerRouter = require('./routes/api');

//Mediante la función use añadimos, las nuevas rutas
app.use('/api', layerRouter); 

```

Reiniciamos nuestra aplicación con *node server.js*.

Para comprobar si nuestra aplicación cumple su cometido escribimos en nuestro navegador [http://localhost:3000/api/layers/layer](http://localhost:3000/api/layers/layer)


![Drag Racing](/images/blog/201909_apirest/07_get_layer.png)

Podemos guardar los datos en nuestro equipo con la extensión geojson (ej. alojamientosdera.geojson), pero también podemos pintar los datos de forma sencilla copiando el texto y pegándolo en la aplicación web [geojson.io](http://geojson.io)

![Drag Racing](/images/blog/201909_apirest/08_geojsonio.png)


El proyecto final se encuentra en [GitHub](https://github.com/sigdeletras/geoapi).
