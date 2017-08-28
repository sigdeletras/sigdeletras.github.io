---
title:  "CDAU Downloader. Plugin de QGIS para la descarga del Callejero de Andalucía"
comments: true
excerpt_separator: "<!--more-->"
header:
  teaser: "/images/header/2017-08-28-img_cabecera_cdau.png"
related: true
categories: 
  - 2017
  - Blog
tags:
  - Callejero
  - Andalucía
  - Python
  - QGIS
  - Plugins
---

Continuando con la filosofía del plugin [Spanish Inspire Catastral Downloader](http://www.sigdeletras.com/2017/blog/plugin-de-qgis-para-descarga-de-datos-catastrales-inspire/) y aprovechando el código generado, he programado el complemento para QGIS **CDAU Downloader** (...es verdad, no me he estrujado mucho la cabeza para el nombre ;-).

La idea es poder descarga desde el SIG de escritorio [QGIS](http://www.qgis.org/es/site/), las capas del proyecto [CDAU, Callejero Digital de Andalucía Unificado](http://www.callejerodeandalucia.es/portal/web/cdau/). Además de ser la base para cualquier proyecto SIG que necesite una capa de viales y direcciones postales de un municipio de Andalucía, hace un par de años tuve la oportunidad de conocer a fondo este ambicioso proyecto de la Junta de Andalucía y colaborar a ponerlo en marcha en el [Ayuntamiento de Roquetas de Mar](http://www.telealmerianoticias.es/2016/roquetas-de-mar-gestion-de-la-ciudad-culmina-el-callejero-unificado-que-se-pondra-a-disposicion-publica-235040.html) (Almería).

## Algunos dato sobre el Callejero Digital de Andalucía Unificado

La información geográfica del CDAU es accesible desde distintos servicios OGC (WMS y WFS). Incluso puede ser descargada por municipio desde la misma [web](http://www.callejerodeandalucia.es/portal/web/cdau/cdau;jsessionid=11EEA3601F82237365A5A8335242CE96). En nuestro caso, el plugin aprovecha las posibilidades del servicio WFS para la descarga de las capas directamente desde el SIG. 

La calidad de las capas del CDAU es relevente, ya que cuenta con el apoyo de aquellas entidades que generan y mantienen estos datos, o sea los ayuntamientos o en su defecto las diputaciones provinciales. 

Disponer de estas capas en nuestro proyecto nos permitirá realizar labores de geocodificación de datos a direcciones postales, tramos o viales completos. Este tipo de geodatos es fundamental en cualquier administración pública, pero sin duda tiene un papel fundamental para empresas de logística (*routing*), gestión inmobiliaria o geomarketing...

Es importante reseñar que la licencia de uso general es la CC BY 4.0 que *implica la autorización para la reutilización de la información en condiciones no restrictivas, siendo posible la copia, distribución y comunicación pública, así como la producción de obras derivadas, incluso con finalidad comercial citando la autoría de la fuentes*. 

Las capas geométricas disponibles son:

* **Vial** . Entidad lineal que representa el eje de vía. Se incluyen tanto vías urbanas (calles, avenidas, plazas, etc.) como interurbanas (autovías, carreteras, caminos, etc.). Los tres datos principales de una vía son su código INE y su nombre. 

* **Tramo**. Entidad lineal básica de un callejero en la que puede descomponerse una vía.

* **Portalero/PK**. Representa de forma puntual portales, puntos kilométricos y portales en diseminado y está asociado a una única vía. Los principales atributos de la tabla portalpk son: número de portal desde, número de portal hasta, extensión desde, extensión hasta, bloque, portal y escalera. Los puntos también están vinculados a un núcleo de población, código postal y sección censal.

## Uso del plugin

### Instalación

La extensión puede ser instalada desde el menú <b>Complementos>Administrar e instalar complementos</b> de QGIS. Para localizar de forma rápida el complemento puede introducirse el término <i>"CDAU"</i> en la herramienta de búsqueda.

<img src="/images/blog/201708_cdau/search.PNG" width="70%">

### Descarga de capas

Tras su instalación, el plugin puede ser ejecutado desde la barra de herramientas o bien desde el menú <b>Complementos>Descarga Callejero CDAU</b> o bien <b>CDAU Downloader</b> si tenemos instalado QGIS en otro idioma.

<img src="/images/blog/201708_cdau/ui.PNG" width="50%">

Una vez ejecutado el complemento se debe <b>obligatoriamente</b>:
<ul>
<li>Seleccionar una provincia de Andalucía.</li>
<li>Seleccionar el municipio.</li>
<li>Indicar la carpeta de descarga.</li>
<li>Indicar las capas a descargar.</li>
</ul>

El plugin hará las correspondientes peticiones al servicio [WFS](http://www.callejerodeandalucia.es/portal/web/cdau/descarga "Información sobre el servicio WFS") y descargará las capas en formato **GeoJSON** en la carpeta indicada. **El sistema de referencia de las capas es ETRS89 (EPGS:4258)**.

Se ha incluído la posibilidad de **añadir simbología básica a las capas** *Vial* y *Portalero/PK*. La simbología incluye:

* Capa **Vial**: Color negro y etiquetado por nombre de calle (campo *"nom_normalizado"*) visible a partir de la escala 1:5000

* Capa **Portal/PK**: Visibilidad de la capa capa a partir de la escala 1:3000, simbología puntal y etiquetado por número (campo *"num_por_desde"*)

<figure>
    <img src="/images/blog/201708_cdau/cdau_simbologia_qgis.png" alt="Opción simbología de capas"  title="Opción simbología de capas"  width="100%">
    <figcaption><i>Comparativa de carga de capas con o sin simbología. Roquetas de Mar (Almería). Base PNOA</i></figcaption>
</figure>

Aunque el conjunto de datos está limitado a la comunidad autónoma andaluza, espero que este complemento pueda ser de utilidad. Igualmente, todo el código Python disponible en el repositorio GitHub puede ser adaptado para otros servicios WFS.
