---
title:  "Probando la nueva versión de QGIS 3 (bueno 2.99)"
comments: true
excerpt_separator: "<!--more-->"
header:
  teaser: "/images/header/2017-08-04_qgis3.PNG"
related: true
categories: 
  - 2017
tags:
  - QGIS
gallery:
  - url: /images/blog/201709_qgis299/qgis_data_source_manager.PNG
    image_path: /images/blog/201709_qgis299/qgis_data_source_manager.PNG
    alt: "QGIS 2.99 Fomrulario de orígenes de datos"
    title: "QGIS 2.99 Fomrulario de orígenes de datos"
  - image_path: /images/blog/201709_qgis299/qgis_edicion.png
    alt: "QGIS 2.99 Ayudas para la edición geométrica"
    title: "QGIS 2.99 Ayudas para la edición geométrica"
  - image_path: /images/blog/201709_qgis299/qgis_simbologia.PNG
    alt: "QGIS 2.99 Nuevas simbologías"
    title: "QGIS 2.99 Nuevas simbologías"
  - image_path: /images/blog/201709_qgis299/qgis_opcionesguardar.PNG
    alt: "QGIS 2.99 Mejoras Guardar como imágen/PDF"
    title: "QGIS 2.99 Mejoras Guardar como imágen/PDF"   
---

Según la [hoja de ruta del proyecto](https://www.qgis.org/es/site/getinvolved/development/roadmap.html "QGIS roadmap"), **a mediados de septiembre estará disponible la versión 3 del Sistema de Información Geográfica QGIS**. Aunque la versión se encuentra en su fase de desarrollo, ya podemos encontrar  entradas y  [videos](https://www.youtube.com/results?search_query=qgis+3) que nos muestran algunas de los futuros cambios y nuevas funcionalidades. 

El gran cambio desde el punto de vista de desarrollo será el uso de Python 3, Qt5 y PyQt5.  Esto provocará un gran cambio, o ruptura, en la [API de QGIS](http://doc.qgis.org/api/api_break.html "API Break") y  supondrá un importante impacto en todo lo vinculado con la programación,  scripts con PyQGIS o plugins. En nuestro caso, los plugins para la descarga de [Catastro Inspire](http://www.sigdeletras.com/2017/blog/plugin-de-qgis-para-descarga-de-datos-catastrales-inspire/ "Spanish Inspire Catastral Downloader. Plugin de QGIS para descarga de datos catastrales INSPIRE") y el [callejero de Andalucía](http://www.sigdeletras.com/2017/blog/cdau-downloader-plugin-de-qgis-para-la-descarga-del-callejero-de-andalucia/ "CDAU Downloader. Plugin de QGIS para la descarga del Callejero de Andalucía") ya se encuntran preparados para ser probados en la nueva versión. 

Sobre este tema puede ser interesante revisar la presentación de [Nyall Dawson](http://nyalldawson.net/) en la pasada conferencia internacional de QGIS que tuvo lugar el pasado Agosto en Nødebo Dinamarca. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/TcZd1Y_ISi4" frameborder="0" allowfullscreen></iframe>

## ¿Cómo probar QGIS 2.99 en Windows?

Aunque la versión no está lanzada oficialmente, si queremos ir viendo algunos de los nuevos cambios podemos instalar de forma conjunta con nuestro QGIS 2.18/2.14 esta versión. Para **probar la versión de desarrollo en Windows** tenemos dos opciones:

- Descarga desde [esta dirección](http://qgis.org/downloads/weekly/?C=M;O=D) el ejecutable acorde a nuestra arquitectura e instalarlo. 

![Repositorio de descarga](/images/blog/201709_qgis299/descarga_ejecutable.PNG)

- Si hemos instalado nuestro QGIS usando [OSGeo4W](https://qgismx.wordpress.com/2016/10/10/instalacion-avanzada-de-qgis-con-osgeo4w/ "Instalación Avanzada de QGIS con OSGeo4W"):

	- Ejecutar el programa "Setup" de OSGeo4W.

	- Marcar la opción "Advanced Install".

	- Aceptar las opciones por defecto.

	- En el formulario Selección de paquetes (Select packages), localizar el paquete **qgis-dev** (categoría Desktop) y marcarlo para su instalación.

	- Con toda seguridad, el instalador nos avisará que se necesitan añadir algunas dependencias que aceptaremos.

![Búsqueda de qgis-dev](/images/blog/201709_qgis299/paquetes.PNG)

## Algunas novedades

La instalación de QGIS en Windows mediante OSGeo4W también nos permitirá actualizar nuestro QGIS estable, sin necesidad de desistalar.

Una vez instalado podemos ir "curiosando" algunas de las mejoras como:

- El gestor de orígenes de datos.
- Los nuevos estilos de simbología.
- La instalación de complementos mediante archivos ZIP
- Las ayudas para la edición de geometrías (segementos y nodos).
- Las nuevas opciones de salvar guardar imágenes o PDFs.
- El buscador de herramientas.
- Panel de hacer/deshacer ediciones.

{% include gallery caption="Capturas de nuevas funcionalidades en QGIS 2.99." %}

