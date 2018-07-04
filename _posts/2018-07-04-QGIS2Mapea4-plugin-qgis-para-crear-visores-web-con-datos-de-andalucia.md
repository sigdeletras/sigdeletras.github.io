---
title:  "QGIS2Mapea4. Plugin de QGIS para crear visores web con datos de Andalucía"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201807_qgis2mapea4/qgis2mapea4.png" 
categories: 
  - 2018
tags:
  - SIG
  - QGIS
  - Andalucía
  - Python
  - Webmapping
---

Es habitual que cualquier proyecto realizado con un Sistema de Información Geográfica termine con una presentación, ya sea en forma de informe y planos adjuntos, de los resultados del trabajo. Junto a esta difusión de resultados más clásica, la presentación de datos geoposicionados en web mediante visores de mapas dinámicos, completa las posibilidades que las Tecnologías de Información Geográfica nos ofrecen para dar a conocer un determinado conjunto de datos espaciales.
<!--more-->
Una buena muestra de estas posibilidades, la tenemos en numeroso conjunto de aplicaciones y tecnologías con la que hoy día contamos. Servicios como Carto, Google Maps, herramientas tipo GeoWE, ArcGIS online, Instamaps son algunas de ellas. Os recomiendo el artículo Paulino Vallejo titulado “10 aplicaciones GIS en la nube para publicar mapas” publico en MappingGIS para un completa visión sobre esta panorama.

Si estos servicios y tecnologías no son suficientes, contamos con librerías JavaScript de mapas, como OpenLayers o Leaflet, para desarrollar aplicaciones web a medida que se ajusten a nuestra necesidades. Estos paquetes abiertos están cogiendo cada vez más fuerza, sobre todo tras la reciente [modificación de las condiciones](https://elandroidelibre.elespanol.com/2018/05/google-maps-cambia-apis-desarrolladores.html) de usos de la API de Google Maps. 

En estos últimos años, van apareciendo también proyectos de administraciones públicas, que partiendo del código de librerías como OL o Leaflet, crean sus  propias APIS, que simplifican, mejoran o personalizan estos paquetes para el desarrollo de mapas en la web. Estas iniciativas están pensadas para facilitar a los responsables técnicos, normalmente informáticos, de las distintas administraciones la publicación web de datos geográficos mediante mapas embebidos, según unas pautas de imagen corporativa, ajustando los datos a un ámbito geográfica y agilizando el uso de servicios estándar  de mapas propios como pueden ser callejeros, mapas base, ortoimágenes. Sirva como ejemplo, [API js de La Rioja](https://iderioja.github.io/doc_api_iderioja/), [GeoEuskadi](http://www.geo.euskadi.eus/api-geoeuskadi-ejemplos-del-visor/s69-geocont/es/), [IDE Menorca](http://cartografia.cime.es/Contingut.aspx?MENU=Geoserveis&IdPub=155), [IGN Carto Visor](http://www.cartociudad.es/VisualizadorCartografico/), la [IDE de la provincia de Málaga](http://www.idemap.es/idemap/api/) o la  [API SITNA](http://sitna.navarra.es/geoportal/recursos/api.aspx)

![Ejemplo con la API de la IDE de La Rioja](/images/blog/201807_qgis2mapea4/apirioja.png)

*Ejemplo con la API de la IDE de La Rioja*

# Mapea4, API de mapas para Andalucía

Dentro del proyecto del SIG Corporativo de la Junta de Andalucía, se encuentra al API Mapea4. Mapea4 es una API basada en OpenLayer que corresponde al la última versión en el que se basa [Mapea](http://www.ideandalucia.es/portal/web/ideandalucia/herramientas/mapea) una herramienta para la inserción de visores cartográficos en paginas web. En la por alguna de las páginas de la web de la Junta de Andalucía habrá una posibilidad alta de encontrarnos  algún mapa realizado con Mapea.

![Mapea](/images/blog/201807_qgis2mapea4/ejemplo_mapea.png)

*Mapea*

Mapea4 cuenta con dos APIs:

- A través de una API REST muy sencilla y documentada permite incluir un visualizador interactivo en cualquier página web sin necesidad de disponer de conocimientos específicos en programación ni en el ámbito de los SIG.
- A través de una API JavaScript que permite crear desde visualizadores de mapas básico hasta otros de mayor complejidad.

El código de Mapea4, junto a una wiki sobre la API se encuentra en un [respositorio de GitHub](https://github.com/sigcorporativo-ja/Mapea4). Desde la wiki se puede consultar todas las posibilidades que esta API posee incluyéndose enlaces a ejemplos en [JSFiddle](http://jsfiddle.net/user/sigcJunta/fiddles/)

![Repositorio de Mapea4](/images/blog/201807_qgis2mapea4/repositorio_mapea.png)

*Repositorio de Mapea4]*

# El *pluging* QGIS2Mapea4

A pesar del gran esfuerzo que conlleva realizar estos desarrollos y la disponibilidad de códigos de ejemplo de cómo generar mapas con algunas de estas API, como no se tengan conocimientos básicos e HTML, JavaScript y CSS, la generación de estos visores esta labor no es tan sencilla. Cada vez es más frecuente encontrar usuarios SIG que empiezan a tener conocimientos de programación, sobre todo en Python, pero son los menos, a nos ser que hayan realizados estudios específicos de informática, los que dan el salto al desarrollo de aplicaciones web.

Bajo esta filosofía, con la finalidad de facilitar al usuario SIG, en concreto al usuario de QGIS, he creado el complemento QGIS2Mapea4, que permite crear desde QGIS 3 un visor sencillo a partir de una capa vectorial con datos ubicados en la comunidad autónoma de Andalucía usando la API Mapea4.

Creo que el desarrollo de este tipo de complementos, es de gran utilidad para poder acercar al usuario estas herramientas. Con esta mismos filosofía se crearon otros dos complementos para QGIS que han tenido muy buena acogida: [CDAU Downloader](http://www.sigdeletras.com/2017/blog/cdau-downloader-plugin-de-qgis-para-la-descarga-del-callejero-de-andalucia/) y [Spanish Inspire Catastral Downloader](http://www.sigdeletras.com/2017/blog/plugin-de-qgis-para-descarga-de-datos-catastrales-inspire/). En estos casos el objetivo fue el de facilitar la descarga de datos geográficos base como son los de catastro o los callejeros.

## Instalación QGIS2Mapea4

Para probar QGIS2Mapea4 es necesario tener instalado [QGIS 3](https://www.qgis.org/es/site/). La forma sencilla de instalar el complemento es desde el **Administrador de Complementos de QGIS**. La otra forma es descargar o clonar el [repositorio de GitHub](https://github.com/sigdeletras/qgis2mapea4) e instalar directamente el zip. Esta opción es nueva desde la versión QGIS 3.

## Usos y opciones

Ejecutando el complemento desde el nuevo icono añadido o desde el menú Web, aparecerá un formulario con las distintas opciones del complemento.

![Formulario](/images/blog/201807_qgis2mapea4/formulario.png)

*Formulario de QGIs2Mapea4*

- **Nombre de la capa**. Se podrá añadir el nombre de la capa que aparecerá en el visor.
- **Proxy**. Activa o desactiva el proxy de la API. 
	- *Desactivado*: Para archivos en local.
	- *Activado*: Para archivos en servidor.
- **Selección de capa vectorial**. Presenta un desplegable con las capas desplegables cargadas en el proyecto de QGIS. En el caso de tener elementos seleccionados permite crear el visor solo con ellos.
- **Ubicación de archivos**: Directorio local donde se creará la carpeta con los ficheros del visor.
- **Mapas base**: Permite seleccionar los mapas base del visor. En esta versión son los datos del proyecto de Callejero Digital de Andalucía Unificado (CDAU), ortoimagen y/o combinación de ambos.
- **Opciones del visor**. Permite añadir distintas opciones y herramientas al visor incluidas en Mapea4
- **Complementos**: Al API permite añadir un conjunto variado de [complementos](https://github.com/sigcorporativo-ja/Mapea4/wiki/Plugins).

Gracias a Mapea4, se puede de forma automática acceder a los atributos de la capa publicada simplemente haciendo clic en alguna de las geometrías.

![Atributos](/images/blog/201807_qgis2mapea4/info_popup.png)

## Añadir el visor a nuestra web.

La carpeta generada puede ser subida directamente a nuestro hospedaje web. Accediendo a nuestro dominio y completando con la ubicación de los ficheros tendremos la dirección del visor. Por ejemplo, hemos creado un visor con QGIS2Mapea4 en la carpeta ejemplos de nuestro hospedaje. La dirección de acceso es por tanto http://sigdeletras.com/ejemplos/index.html. Esta dirección accede al visor a pantalla completa

Podemos también añadir el visor a una publicación de nuestra web o blog. Una vez subidos los archivos del visor, debemos acceder a modo HTML de nuestra entrada y insertar el código mediante las etiquetas HTML que se llaman <iframe>

El código de ejemplos y el resultado lo tenéis a continuación.

	<iframe width="525" height="350" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" 
	src="http://www.sigdeletras.com/qgis2mapea4/poblamiento_roquetas/"> </iframe> 

<iframe src="http://www.sigdeletras.com/qgis2mapea4/poblamiento_roquetas/" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> 

*<a href="http://www.sigdeletras.com/qgis2mapea4/poblamiento_roquetas/" target="_blank">Ver a pantalla completa</a>*

# Conclusión

La idea de crear un plugin para QGIS que genere el código de un visor web no es novedoso. Existe ya desde hace un tiempo un magnífico complemento llamado [QGIS2Web}(https://plugins.qgis.org/plugins/qgis2web/) que tiene muchísimas más prestaciones que este modesto complemento. Solo hay que ver el equipo de desarrolladores para ver su potencial.

El objetivo de nuestro complemento es simplemente poner en marcha una idea que creemos puede ser de interés para los usuarios que trabajan con datos ubicados en Andalucía, revisar las posibilidades de la nueva API de QGIS3 y poner un ejemplo de cómo acercar este tipo de desarrollos al usuario SIG.

Sin duda hay gran parte de las opciones de Mapea4 que no han sido incorporadas. El desarrollo de este complemento no está vinculado con ninguna administración pública y han sido incorporadas una selección de las herramientas básicas que pueden conformar un visor de mapas en la web. 

Con todo esto, indicar que el complementose encuentra bajo licencia GNU General Public License y que puede ser mejorado por la comunidad. En el caso de algún desarrollo particular siempre podemos ponernos en contacto. 


