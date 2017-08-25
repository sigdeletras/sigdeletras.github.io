---
title:  "Spanish Inspire Catastral Downloader. Plugin de QGIS para descarga de datos catastrales INSPIRE"
comments: true
excerpt_separator: "<!--more-->"
header:
  teaser: "/images/header/2017-07-21-img_cabcera_plugin.jpg"
related: true
categories: 
  - Blog
  - 2017
tags:
  - Catastro
  - España
  - Python
  - QGIS
  - Plugins
---

Hoy por hoy, podemos afirmar que en España nos encontramos en un buen momento respecto al acceso a la Información Geográfica. Existen numerosos [geoportales oficiales para la descarga](http://www.idee.es/web/guest/centros-de-descarga) de cartografía de referencia y temática. El número de [servicios de mapas interoperables](http://www.idee.es/web/guest/directorio-de-servicios) accesibles desde las IDEs es bastante numeroso. Los propios usuarios cuentan con proyectos como [OpenStreetMap](https://www.openstreetmap.org/) para generar datos a escala mundial. Y por último, hay que  tener en cuenta que podemos acceder mediante sus API a los datos geolocalizados de determinadas aplicaciones, ej. [Twitter](https://dev.twitter.com/rest/reference/get/geo/search).

<!--more-->

Frente a esta variedad de fuentes, es interesante contar con herramientas que permitan la adquisición ágil de estos georrecursos. Con esta finalidad se ha creado el **complemento para el SIG de escritorio QGIS "****Spanish Inspire Catastral Downloader****" para la descarga de los conjuntos de datos catastrales según INSPIRE de España** y que ya está disponible en el repositorio oficial de plugins de QGIS.

### Los complementos de QGIS

Dentro del mundo geo, es indiscutible que [QGIS](http://www.qgis.org/es/site/) es uno de los SIG de escritorio de código abierto más usados. Si fueran poco las funcionalidades y procesos que el programa trae por defecto, éstas pueden verse ampliadas mediante la instalación de plugins o complementos creados por la comunidad.[página oficial de plugins de QGIS](https://plugins.qgis.org/plugins/).

Junto a estos complementos de acceso público, hay que tener en cuenta los <span style="text-decoration: underline;">desarrollos a medida</span> que tanto empresas como profesionales del sector pueden desarrollar para proyectos o encargos privados. Esta está siendo una de las <span style="text-decoration: underline;">líneas de negocio principales vinculadas al trabajo con tecnologías de información geográfica de código abierto</span>.

### El plugin "Spanish Inspire Catastral Downloader"

Desde hace ya unos años, tanto los datos geográficos en formato Shape como los datos CAT de Catastro pueden ser descargados mediante certificado digital desde la página de la [Sede Electrónica de Catastro](https://www.sedecatastro.gob.es/OVCFrames.aspx?TIPO=TIT&a=masiv). Sobre el uso de estos datos se pueden consultar las [entradas siguientes](2016/uso-de-la-informacion-catastral-para-estudios-urbanos/itemlist/tag/catastro).

A este recurso, se añadió recientemente los [Servicios de Cartografía Catastral según Inspire](http://www.catastro.minhap.es/webinspire/index.html) que ofrece la Dirección General de Catastro. La información catastral adaptada a la directiva europea Inspire es ofrecida mediante servicios interoperables (WMS y WFS) y puede realizarse la descarga de los tres conjuntos de datos (Parcelas Catastrales, Edificios y Direcciones) mediante un servicio ATOM. Cada conjunto de datos , distribuidos en archivos ZIP,  contiene varias capas en formato GML, en el sistema de referencia ETRS89 y son descargados por municipios.

<!-- ![Apartado de servicio ATOM de datos catastrales INSPIRE](/images/blog/201707_plugin/atom.PNG) -->
<!-- _Apartado de servicio ATOM de datos catastrales INSPIRE_ -->
<figure>
  <img src="/images/blog/201707_plugin/atom.PNG" alt="Apartado de servicio ATOM de datos catastrales INSPIRE">
  <figcaption>Apartado de servicio ATOM de datos catastrales INSPIRE.</figcaption>
</figure>

Los archivos geográficos (GML) contenidos en cada conjunto de datos son:

*   Conjunto de Datos de **Parcela Catastral** **(CP Cadastral Parcel)**
	*   CadastralParcel. Parcela catastral.
	*   CadastralZoning. Manzanas en suelo urbano o a los polígonos en suelo rústico.
*   Conjunto de Datos de **Edificios (BU Buildings)**
	*   Building. Edificio.
	*   BuildingPart. Cada una de las construcciones de una parcela catastral que tiene volumen homogéneo, y pueden ser sobre y bajo rasante.
*   OtherConstructions. Piscinas que contienen el atributo OtherConstructionNatureValue calificado cómo openAirPool.
	*   Conjunto de Datos de **Direcciones (AD Addresses)**
	*   Address. Geometría del punto donde georreferencia la dirección física (centroide de la parcela o entrada del portal)

El PDF con la descripción completa de la estructura de datos puede consultarse en el siguiente [enlace](http://www.catastro.minhap.es/webinspire/documentos/Conjuntos%20de%20datos.pdf).

La descarga mediante ATOM pasa por : la selección de conjunto de datos, selección de provincia, municipio, descarga, descompresión y carga en SIG. Este proceso es sin duda poco operativo. Para solventar este escollo, y si trabajamos con QGIS, se puede utilizar el complemento.

### Instalación y uso

El complemento puede ser instalado desde el menú **_Complementos>Administrar e instalar complementos de QGIS_**. Para localizar de forma rápida el complemento puede introducirse el término "catastro" en la herramienta de búsqueda.

<!-- ![Búsqueda del complemento en QGIS](/images/blog/201707_plugin/search.PNG "Búsqueda del complemento en QGIS")
_Instalación del complemento desde QGIS_ -->
<figure>
  <img src="/images/blog/201707_plugin/search.PNG" alt="Búsqueda del complemento en QGIS">
  <figcaption>Búsqueda del complemento en QGIS.</figcaption>
</figure>

Los archivos están igualmente disponibles en un [repositorio de GitHub](https://github.com/sigdeletras/Spanish_Inspire_Catastral_Downloader) y pueden descargarse directamente y copiarlos en la carpeta de _plugins_.

Tras su instalación el plugin puede ser ejecutado desde la barra de herramientas o bien desde el menú **_Complementos>Descarga Catastro_** _**Inspire**_.  Si tenemos instalado QGIS en otro idioma la opción del menú es _Spanish Inspire Catastral Downloader ._

<!-- ![Formulario de opciones del complemento](/images/blog/201707_plugin/ui.PNG)
_Formulario de opciones_ -->
<figure>
  <img src="/images/blog/201707_plugin/ui.PNG" alt="Formulario de opciones del complemento">
  <figcaption>Formulario de opciones del complemento.</figcaption>
</figure>

Una vez ejecutado el complemento se debe obligatoriamente:

*   Seleccionar la provincia
*   Seleccionar el municipio
*   Indicar la ruta local de descarga
*   Indicar el conjunto de capas a descargar: Parcelas Catastrales, Edificios y/o Direcciones.

Si se desea añadir las capas GML descargadas al proyecto QGIS activo se debe marcar la casilla correspondiente.

<!-- ![Carga de capas en proyecto QGIS](/images/blog/201707_plugin/cadastral_layers.PNG)
_Ejemplo de carga de capas en proyecto QGIS_ -->
<figure>
  <img src="/images/blog/201707_plugin/cadastral_layers.PNG" alt="Ejemplo de carga de capas en proyecto QGIS">
  <figcaption>Ejemplo de carga de capas en proyecto QGIS.</figcaption>
</figure>

### Agradecimientos

En todos las primeras veces, si cuentas con ayuda y orientación mejor. Quisiera agradecer a la [comunidad de usuarios QGIS en español](http://osgeo-org.1560.x6.nabble.com/QGIS-es-f5092059.html), en concreto a [Fran Raga](https://all4gis.github.io/), [Luigi Pirelli](https://www.linkedin.com/in/luigipirelli/?locale=es_ES), [Raúl Nanclares](https://www.linkedin.com/in/raulnanclares/) y [Francisco Pérez Sampayo](https://www.linkedin.com/in/francisco-p%25C3%25A9rez-sampayo-ba305037/), los comentarios, aportes y mejoras de código realizadas.
