---
title:  "Acceso a servicios OGC (WMS,WFS..) con Postman"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201912_postman/portada.png" 
categories: 
  - 2019
tags:
  - web
  - servicios OGC
---

![html](/images/blog/201912_postman/portada.png)

Sin duda cada día son más numerosos los recursos que ofrecen información geográfica. Además de poder descargar un sinfín de capas de web oficiales, portales de datos abiertos o proyectos como OpenStreetMap, contamos con todos los datos que nos ofrece los **servicios OGC interoperables** que suelen estar recogidos en las páginas de las Infraestructuras de Datos Espaciales.

Normalmente estos servicios son consumidos desde un Sistema de Información Geográfica o través de un visor de mapas web. Esta acercamiento mediante  interfaz gráfica hace que no necesitemos profundizar en la parte técnica del servicio. En mi opinicón se está perdiendo la posibilidad de que estos servicicios sean más explotados, por empresas no geo. Por ejemplo, una **empresa eléctrica podría obtener información sobre la red de suministro eléctrico y la luminaria desde en servicio WFS** para poder tener los datos necesarios para presentarse a una licitación. En este caso no sería necesario presentar los datos en un mapa. Solo queremos obtener dicha información para un informe. Podemos consumir los servicios geográficos como una API. Otra posibilidad puede ser la integración en otros sistemas. Por ejemlo podemos **ofrecer servicios de gestión inmobiliaria y almacenar la referencia catastral de los inmuebles**. Para todar de componente espacial a los datos podrí vincularse nuestro ERP para añadir los datos catastrales públicos a partir del **WMS de Catastro** u obtener la representación gráfica para añadirlos a un visor de la aplicación.

En lo que espero sea una pequeña serie de entradas voy intentar explicar con algo más de detalle técnico en que consisten estos servicios web datos geográficos y **cómo podrían usarse las distintas peticiones y datos obtenidos dentro de una aplicación usando herramientas no puramente geográficas como Postman**.

## Peticiones HTTP a servicios OGC

Al consumir un servicio web OGC, lo que estamos es realizando una consulta (petición/request) mediante  un cliente (navegador, SIG..) al servidor donde está alojando el servicio. Una vez realizada dicha petición, el servidor nos devuelve respuesta (response) que será interpreada por nuestro cliente. Según el tipo de servicio, la respuesta podrá ser una imagen o conjunto de imáges georrerenciadas si el servicios es de tipo WMS ([Web Map Service](https://www.opengeospatial.org/standards/wfs)) o bien, una colección de objetos con información geográfica y atributos en un formato concreto (xml, text/html, json...) si la petición se ha hecho a un servicio WFS ([Web Feature Service](https://www.opengeospatial.org/standards/wms)). Hay más tipo de servicios OGC (ej. WCS o servicio de coberturas), incluso aquellos que van a permitir crear o actualizar objetos geográficos (WFS-T).

Toda esta comunicación se realzia mediante el [protocolo HTTP](https://developer.mozilla.org/es/docs/Web/HTTP/Overview) que permite la comunicación en la WWW. Existe varios tipos de peticiones HTTP. Las más usadas son las de tipo GET. Por ejemplo cuando queremos consultar los metadatos de uservicio WMS realizamos la petición GET llamada *GetCapabilitie*s o para obtener un objeto usamos GetFeature. El protocolo HTTP tiene muchas otras peticiones POST, PUT, DELETE... pero para consumo de servicios geo nos centraremos en las de tipo GET.

## Peticiones desde el navegador o usando curl

Como he comentado en la mayoría de las ocasiones las consultas a nuestros servicios van a ser realizadas con un Sistema de Información Geográfica (SIG) o con un visor de mapas web que lo tenga implementado, por ejemlo usando librerías JavaScript como OpenLayers o Leaflet. Esto no quiere decir que no podamos **realizar una petición directamente desde un navegador, o incluso desde un terminal** de nuestro equipo siempre que estemos conectados a Internet.

Así, si copiamos la siguiente URL en nuestro navegador, obtendremos los metadatos del servicio [WFS de la Encuesta de Infraestructuras y Equipamientos suministrado por la Diputación de Córdoba](https://www.dipucordoba.es/servicios_geoportal). 

```
https://mapserver.eprinsa.es/cgi-bin/eiel_wfs?service=WFS&version=1.1.0&request=GetCapabilities
```

![Petición navegador](/images/blog/201912_postman/03_peticion_navegador.png)

De igual manera desde el terminal de nuestro equipo, podemos usar el comando [curl](https://curl.haxx.se/) y realizar la misma petición.

```
curl -X GET 'https://mapserver.eprinsa.es/cgi-bin/eiel_wfs?service=WFS&version=1.1.0&request=GetCapabilities'
```
![Petición cliente](/images/blog/201912_postman/03_peticion_cliente.png)

## Usando Postman para nuestras peticiones

Podemos usar una aplicación que nos dote de una interfaz gráfica (GUI) para realizar las consultas. Existen varias opciones, desde complementos para los distintos navegadores, a programas que podemos instalar en nuestro equipo como Postman io  [Insomnia](https://insomnia.rest/)).

**Postman** es una herramienta que se utiliza para realizar pruebas sobre servicios API REST. Una vez instalado, podemos crear una colección de peticiones, guardar variables y definirlas dentro de distintos entornos (desarrollo, producción, testing...) y compartir con otros usuarios o miembros de nuestro equipo la colección. Podemos crear nuestras peticiones añadiendo los parámetros de forma gráfica y ver los resultados en distintos formatos (xml, json, html...). Otra opción interesante es la de poder obtener el código base para generar la petición en distintos lenguajes de programación (Pyhon, Java, Javascript, Nodejs, Ruby, PHP) y guardar los resultados como fichero. [Postman]((https://www.getpostman.com/)) puede ser usado desde la web  si lo deseamos instalarlo localmente. Las ejemplos de la entrada están realizados sobre la aplicación local. 

Una vez que nos hemos instalado Postman, lo abriremos y creamos una un espacio de trabajo (**workspace**) que se llamará *Servicios EIEL Córdoba*.

![Wordspace](/images/blog/201912_postman/05_workspace.png)

La primera peticion que vamos a realizar es la que hemos usado en el apartado anterior. La pegamos en la entrada donde indica *Enter request URL*. Veremos como se completan cada uno de los parámetros de la petición. Esto nos va a permitir modificarlos o añadir más forma muy sencilla. Una vez creada la petición, la vamos a ejecutar haciendo clic en *Send*. Si todos los datos son correcto, podremos comprobar en la parte inferior el resultado de la petición. Por defecto se presenta en el formato que tenga establecido el servidor. Para servidores OGC el formato es XML. Puede modificarse la vista previa si lo deseamos, siempre que esté permitida o definida en la petición.

En la captura vemos los datos del servicio WFS de los datos del **Sistema de Información Geográfica Provincial de la Diputación de Córdoba**. Los datos corresponden con la EIEL que

*...es un instrumento de análisis cuantitativo y cualitativo de los servicios de competencia municipal. Constituye un inventario de ámbito nacional, de carácter censal, que tiene como objetivo conocer periódicamente la situación y el nivel de dotación de infraestructuras y equipamientos locales, a fin de poder evaluar las necesidades de dichos sectores, permitir una correcta distribución de los recursos, eliminando los desequilibrios regionales mediante una mejor planificación de las inversiones públicas que la Administración Central y Local realiza en los municipios* [Más información](http://www.mptfp.es/portal/politica-territorial/local/coop_econom_local_estado_fondos_europeos/eiel.html)

La Diputación de Córdoba a través del [Sistema de Información Geográfica y Estadística (SIGE)](https://www.dipucordoba.es/sige),soporte tecnológico de EPRINSA,  es el responsable de mantener los servicios geográficos de acceso a la EIEL que constituyen un recurso de mucho interés no solo para la administracione locales sino para los profesionales que lo necesiten

![Petición navegador](/images/blog/201912_postman/06_peticion.png)

Podemos ir guardando las peticiones en colecciones. Si hacemos clic en *Save*, almacenaremos la petición con un título y una descripción dentro de una colección que debemos crear en el caso de que no exista. 

![Guardado de petición](/images/blog/201912_postman/07_guarar_request.png)

## Petición GetFeature

Junto a la petición *GetCapabilities* de acceso a los metadatos, cualquier servicio WFS debe permitir realizar una descripción de los tipos de elementos soportados (*DescribeFeatureType*) y obtener una selección de objetos de la base de datos que incluyan su geometría y atributos (*GetFeature*).

Voy a añadir una nueva petición que nos devuelva las **líneas de alumbrado**. El listado de capas del servicio lo podemos obtener de la petición anterior. Para produndizar más en los distintos parámetros para cada tipo de operación podemos acceder a la [documentación de Geoserver](https://docs.geoserver.org/latest/en/user/services/wfs/reference.html), aunque también podemos consultar el [documento de la especificación](https://www.opengeospatial.org/standards/wfs).

![Capa alumbrado](/images/blog/201912_postman/08_capa_alumbrado.png)

La url completa que vamos a pegar y ejecutar es la siguiente:

```
https://mapserver.eprinsa.es/cgi-bin/eiel_wfs?service=WFS&version=1.1.0&request=GetFeature&typename=ms:ALUMBRADO-Lineas&MAXFEATURES=10
```
Tras ejecutarla podemos ver la vista de la petición que nos presenta en formato XML (GML) los datos correspondientes a las líneas de alumbrado obtenidas que hemos limitado a 100 para agilizar la petición.

![GetFeature](/images/blog/201912_postman/10_getfeature.png)

Podemos ir añadiendo parámetros a la petición. Por ejemplo los datos se ofrecen en EPGS:25830. Si quisiéramos obtenerlos en WGS84 solo deberíamos añadir el parámetro *SRSNAME* seguido del código EPGS correspondiente. En este caso los datos e la EIEL de Córdoba solo se suministran en ETRS89 UTM 30N por lo que la petición devuelve error.

## Filtros

Dentro de la petición también podemos realizar filtros. Los filtros pueden ser de tipo espaciales o lógicos. La petición de metadatos nos indica al final que tipos de filtros son los permitidos. Para más información pueden consultarse los siguientes enlaces [1](https://mapserver.org/ogc/filter_encoding.html), [2](https://docs.geoserver.org/latest/en/user/filter/function.html) o [3](https://www.opengeospatial.org/standards/filter).

![Lenguaje de filtrado](/images/blog/201912_postman/11_filtros.png)

Vamos a añadir un **filtro que nos devuelva las líneas de alumbrado del municipio de Fuente Obejuna**. El filtro sería el siguiente y debemos añadirlo con el parámetro *filter*.

```html
<Filter><PropertyIsEqualTo><PropertyName>municipio</PropertyName><Literal>FUENTE OBEJUNA</Literal></PropertyIsEqualTo></Filter>
```
![Filtro](/images/blog/201912_postman/12_filtro_fuenteobejuna.png)

Podemos sacarle gran utilidad a los filtros tanto si se buscan tanto sobre los atributos (like, E
equalthan, between...), como si usamos operadores espaciales tipo cajas geográficas (BBOX), superposiciones (overlaps), distanta (DWithin)...

## Obtener fichero geográfico

Todas las peticiones que realicemos pueden guardarse en un fichero. Tras ejecutar la consulta anterior, localizamos el botón de **guarda en local el resultado como archivo (Save to a file)**. El formato por defecto es XML, pero nuestras peticiones son en verdad archivos GML por lo que las podemos cargar en nuestro SIG. en la captura siguiente tenemos los datos sobre OpenStreetMap usando QGIS.

![Fichero gml con QGIS](/images/blog/201912_postman/13_qgis.png)

Los servicios WFS permiten obtener las respuestas en otros formatos. Es muy últil por ejemplo **obtener los datos en JSON y así poder usarlos en una aplicación web y cargarlos mediante Ajax por ejemplo**. Para ello debemos añadir el parámetro *outputFormat* y el tipo deseado, siempre que el servicio lo tenga implementado.

![Formtatos de salida](/images/blog/201912_postman/14_outputformat.png)