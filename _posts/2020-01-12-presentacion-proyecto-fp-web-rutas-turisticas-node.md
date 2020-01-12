---
title:  "Presentación del proyecto 'Aplicación web de gestión de rutas turísticas mediante Node.js y API REST'"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202001_fp/portada.png" 
categories: 
  - 2020
tags:
  - web
  - node
  - javascript
  - api rest
---

El pasado 9 de enero tuvo la lugar de la presentación y defensa del proyecto titulado
**"Aplicación web de gestión de rutas turísticas mediante Node.js y API REST"** dentro de los estudios del Ciclo Superior de Desarrollo de Aplicaciones Webs realizados en el [IES Trassierra](http://www.iestrassierra.com/). Con la presentación del mismo, llego al final de un viaje, nada sencillo, que comenzó hace tres años y  que ha desembocado en un cambio profesional relevante.

La justificación principal del proyecto ha consistido en el **diseño de una aplicación web para la de gestión de datos relativos a rutas turísticas y sus puntos de interés**. Este tipo de páginas son propias de empresas que ofrecen visitas guiadas y servicios turísticos. Están teniendo cada vez más auge, sobre todo desde la aparición del concepto de rutas guiadas libres o *[free tour](https://www.muchosol.es/escapes/estos-son-los-mejores-free-tours/)*. Entre las más conocidas se encuentran [civitatis](https://www.civitatis.com/es/), [Freetour](www.freetour.com) o [Weplan](https://www.weplann.com/).

Una de las primeras tareas que realicé fue la de definir **qué quería aprender** durante el tiempo que le iba a dedicar a realizar mi trabajo de fin de ciclo. Me tomé este proyecto como una buena oportunidad para completar la formación recibida durante estos dos años, ver otras tecnologías demandadas en el mercado y afianzar determinados conocimientos sobre todo en la parte "geo". 

Con base a estas ideas, los objetivos formativos y las habilidades técnicas generales que quería conseguir se resumen en estos cuatro puntos.

1. Para completar los conocimientos vistos sobre lenguajes del lado del servidor (PHP y JAVA), quería aprovechar la oportunidad aprender a **programar y desplegar un servidor web basado en JavaScript con [Node.js](https://nodejs.org/es/)**.
2. Poner en marcha una **API Rest** usando [Express.js](https://expressjs.com/es/) para la gestión y consumo de datos.
3. Ya que he trabajado siempre con bases de datos relacionales, el proyecto me daba la oportunidad de poder aprender a manejar  **bases de datos NoSQL** por lo que decidí usar [Mongo DB](https://www.mongodb.com/es) y [Mongoose](https://mongoosejs.com/) como ODM.
4. Y por último, y como no podría ser de otro lugar, quería avanzar en el **manejo, creación y actualización de entidades con componente geográfico** mediante librerías JavaScript ([Leaflet](https://leafletjs.com/)). Podría decir que quería llevar a la web las funcionalidades básicas de edición un SIG de escritorio.

Para saber más sobre el proyecto he dejado una presentación larga desarrollando la metodología usada y haciendo referencia a cada uno de los apartados del trabajo. 

<iframe src="//www.slideshare.net/slideshow/embed_code/key/sGxkikQd7fGRlq" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> 

## Algunas Conclusiones

Creo más interesante aprovechar esta entrada para poder exponer algunas conclusiones y experiencias que me ha llevado este proyecto.

### Servidor Node.js

En relación a la puesta el marcha de un servidor con Node indicar que es bastante sencillo o como comenté en la presentación tiene una curva de aprendizaje corta. Sin embargo, a medida que el proyecto va aumentando en funcionalidades y complejidad, va siendo necesario la instalación de varias dependencias y su consiguiente configuración. 

![Dependencias del servidor Node](/images/blog/202001_fp/01_dependencias_node.png)

*Dependencias del servidor Node.js*

En una de las revisiones con los tutores del proyecto, y coincidiendo con la presentación del sistema de atenticación mediante token usando [JSON Web Tokens (JWT)](https://www.npmjs.com/package/jsonwebtoken), un profesor me comentó que seguro ya existía un *framework* en el que todo esto ya estaba desarrollado. Tras una búsqueda rápida, encontré [Adonis.js](https://adonisjs.com/). Mirando al documentación pensé la gran cantidad de tiempo que me hubiera ahorrado usando este paquete. Pero al momento me di cuenta había llegado a esta conclusión gracias a las horas dedicadas en aprender a montar Node.js desde cero. Sin duda, ahora usaría este o cualquier otro *framework* si tuviera que realizar un trabajo profesional de estas características. Pero sin tener una mínima base sobre Node.js esta parte del proyecto hubiera sido un fracaso si no la huera acometido partiendo de lo mínimo.

El departamento de Informática dota a los alumnos de un dominio y espacio dentro de los servidores para desplegar la aplicación. Este es un requisito obligatorio para poder aprobar el proyecto. Estos espacios están pensados principalmente para proyecto basados en PHP y bases de datos relacionales. En mi caso, debido a los objetivos marcados, tuve que buscar una solución externa para poder subir a producción tanto el servidor, la aplicación y la base de datos. Para ello he utilicé  [Heroku](https://www.heroku.com/) y [Mongo DB Atlas](https://www.mongodb.com) usando las posibilidades que ofrecen las cuentas *freemium*. 

### API Rest

La programación de la  API REST ha sido un gran acierto. La rapidez y la flexibilidad que ha aportado **Express.js** ha favorecido la puesta en marcha rápida de la API. Toda la configuración de los ficheros de rutas, la parametrización de la URLs, la definición de las vistas a renderizar, el servicio de archivos estáticos ha sido sencillo y la página de Express está realmente bien documentada.

En el ciclo vimos como montar servicios con PHP y Java. Al menos  para este tipo de aplicaciones, esta parte ha sido muy "agradecida" si la comparo con los visto en el ciclo. 

![Express](/images/blog/202001_fp/02_express.png)

*Ejemplo de archivo de routes con Express.js*

Como apunte, indicar que probé a acceder a los datos geo de la API desde QGIS y sin problema...

### Base de datos NoSQL

El cambio de paradigma, de relacional a no relacional, me ha provocado cierta dificultad a la hora de desarrollar las consultas de la base de datos, consultas que por otro lado no eran demasiado complejas. Hay que tener muy presente cómo funciona la referencia entre documentos JSON para poder sacar el máximo rendimiento a los datos. La clave de todo esto se encuentra en leer bien la documentación y saber sacarle el máximo rendimiento a Mongoose. 

En la parte geo de los datos comentar que las **formas básicas de representación geográfica estaban identificadas en las entidades de Puntos de Interés o POIs (puntos), rutas (líneas) y zonas (polígonos)**. La geometría de los puntos era almacenada en un par de campos numéricos (longitud y latitud), mientras que las representaciones lineales y poligonales correspondían con *arrays* de pares de números correspondientes con los nodos.

![Objeto JSON con datos geográficos en MongoDB](/images/blog/202001_fp/03_nosql.png)

*Documento JSON (zona) con datos geográficos en MongoDB*

Mongoose da soporte a este tipo de [esquemas geo](https://mongoosejs.com/docs/geojson.html) y permite trabajar con archivos GeoJSON incluso realizar consultas geoespaciales básicas.

### CRUD Geo

Como he comentado he usado **Leaflet** para toda la parte geográfica del proyecto. Se definieron los mapa base sobre los que representar los datos (OpenStreetMap y PNOA) y fueron añadidos los complementos de geolocalización y callejero (Nominatim).

Tanto Leaflet como Openlayers están perfectamente preparadas para poder soportar este tipo de desarrollos, por lo que no hace ninguna falta usar otras librerías de pago.

La parte que más tiempo y lineas de código se ha llevado ha sido la permite la creación y modificación de los elementos geográficos. Todo esto se ha realizado usando [Leaflet Draw](http://leaflet.github.io/Leaflet.draw/docs/leaflet-draw-latest.html) pudiendo por ejemplo, crear los puntos de interés de las rutas sobre el mapa y almacenarlos en la base de datos o poder modificar el trazado de la ruta nodo a nodo.

![Actualización de geometría de ruta con Leaflet Draw](/images/blog/202001_fp/04_leafletdraw.gif)

*Actualización de geometría de ruta con Leaflet Draw.*

En este sentido, al menos para mi, se me abren gran cantidad de posibilidades para trasladar a la web determinadas funciones SIG.

### Front-end

Para el desarrollo de las vistas he usado el motor de plantillas [Handlebars](https://handlebarsjs.com/) y como *framework* CSS [Material Design Bootstrap](https://mdbootstrap.com/). Los resultados han sido satisfactorios, al menos desde el punto de vista del diseño que no es sin duda mi especialidad. 

Gracias el trabajo con token, se ha podido personalizar los elementos que debían presentarse según el rol del usuario (guía o administrador) y al usar un sistema basado en *grid* la aplicación es totalmente *responsive*.

![Vista responsive de la aplicación](/images/blog/202001_fp/05_responsive.png)

*Vista responsive de la aplicación*

De todas formas, creo que esta parte del proyecto podría optimizarse más usando alguno de los *framework* JavaScript actuales tipo Angular, React o Vue.  Es una opción que barajé al principio consultando documentación e  incluso asistiendo a un taller de Vue.js organiza por el Aula de Software Libre de la UCO, pero al final descarté esta idea más que nada por falta de tiempo.

### Pruebas y testing

Para el testeo de los servicios de la API REST se ha usado **Postman** e igualmente se definieron un conjunto de **pruebas de humo (*smoke testing*)** definiendo las funcionalidades básicas (login, alta ruta, edición POI, cambio contraseña...) que debían funcionar correctamente en cada despliegue según el desarrollo realizado en cada sprint.

Al final del proyecto, la API tenía 40 *endpoints* por lo que su testeo con Postman cada vez se iba haciendo más complicado por lo que comencé a ver documentación sobre librerías javascript de testeo como **Mocha y Chai** para el diseño de pruebas unitarias. 

Aunque el proyecto es sencillo respecto a su programación y testeo creo que es fundamental comenzar este tipo de desarrollos basados en la metodología de **Diseño Orientado a Pruebas (TDD)**. El aspecto negativo es haberme dado cuenta cuando esta parte del proyecto ya estaba implementada, pudiendo haber ahorrado tiempo y esfuerzo tiendo todo esto automatizado.

<iframe width="595" height="485" src="https://www.youtube.com/embed/w-af7R4FVzU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
