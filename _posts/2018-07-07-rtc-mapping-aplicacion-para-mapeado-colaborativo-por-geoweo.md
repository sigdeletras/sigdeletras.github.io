---
title:  "RTC Mapping aplicación web de mapeo colaborativo"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201807_rtcmapping/imgentrada.PNG" 
categories: 
  - 2018
tags:
  - Webmapping
---

El pasado jueves 5 de junio tuvo lugar la [XIX Reunión de Geoinquietos Córdoba](https://wiki.osgeo.org/wiki/Reuni%C3%B3n_19_Geoinquietos_C%C3%B3rdoba). A pesar del esfuerzo que supone de convocar y "mover" cada reunión, que sin duda no sería posible sin la ayuda miembros del grupo con Antonio Fernández, son sin duda experiencias de gran interés por todo lo que se aprende y se comparte. Con el tiempo se están convirtiendo en citas ineludibles en Córdoba para todo aquel que de alguna u otra manera se mueva en el mundo geo. 

<!--more-->

En esta ocasión, el tema central de la reunión fue la presentación de la aplicación [RTC Mapping](http://rtcm.geowe.org/), desarrollada por el equipo de la iniciativa [GeoWE](http://www.geowe.org/). La presentación corrió a cargo de [Atanasio Muñoz y José María, que junto a Rafael López](http://www.geowe.org/index.php?id=equipo), son los tres desarrolladores (pilares) de GeoWE. La charla comenzó  una explicación sencilla de qué es RTC Mapping y para qué sirve. Aunque aún se encuentra en su versión Demo 1.0 en la dirección [http://rtcm-app.geowe.org/](http://rtcm-app.geowe.org/), RTC Mapping hace sencillamente lo que debe hacer, permitir a varios usuarios, como si un **Google Doc de mapas** se tratara, crear información geográfica de forma remota y en tiempo real.

![Flayer de la XIX Reunión Geoinquietos Córdoba](/images/blog/201807_rtcmapping/xixgeoinquietos.png)

*Flayer de la XIX Reunión Geoinquietos Córdoba*

Desde su presentación, RTC Mapping ya ha despertado cierto interés. Además de la información en el [blog del proyecto](http://geowegis.blogspot.com/2018/04/mapeo-colaborativo-en-tiempo-real.html), es recomendable el [artículo publicado en MappingGIS por el geógrafo Paulino Vallejo](https://mappinggis.com/2018/05/mapas-colaborativos-en-tiempo-real-con-rtcmapping-de-geowe/) que entra en detalle en las herramientas de la aplicación.

Tras esta introducción, Atanasio y José María se pusieron manos a la obra y mostraron cómo trabaja RTCMapping, enseñando las funciones principales (dibujo y edición geográfica,), capas básicas de apoyo (OpenStreetMap, Bing o Catastro) o la edición de tabla atributos... Sin duda ,el fuerte de RTCMapping es permitir que varios usuarios trabajen de forma simultánea. Atanasio nos enseñó cómo crear una sala de trabajo y activar la opción de Compartir. La url obtenida fue dada a los asistentes y en un momento de la sesión estuvimos hasta 10 personas creando datos a la vez.

![Ata y José María de GeoWE presentando RTCMapping](/images/blog/201807_rtcmapping/atajose.jpg)

*Ata y José María de GeoWE presentando RTCMapping.*

Tras esta primera parte, José María conectó el trabajo realizado con RTCMapping con la aplicación SIG web GeoWE. Pudimos ver cómo terminar de editar los datos generados, trabajar desde directorios GitHub o compartir nuestros mapas en la red. No quiero que se me pase, la referencia que hizo José María al [GeoJson CSS](https://github.com/jmmluna/Leaflet.geojsonCSS) y al complemento para Leaflet por él mejorado que permite trabajar con estilos dentro este formato geográfico estándar.

La reunión continuó con un breve anuncio de una actividad conjunta de la [Asociación de Amigos de Medina Azahara](http://www.amigosdemedinaazahara.com/) y el colectivo Geoinquietos Córdoba. [Curro Crespo](http://www.amasce.co/), arquitecto de Amásce y la arqueóloga Ana Zamorano comentaron el proyecto denominado "Laboratorio de Intervenciones Puntuales" en la que está planteado una inicaitiva de mapeado, análisis y estudio de distintos aspectos del Conjunto Arqueológico de Medina Azahara, recientemente declarado Patriminio de la Humanidad. En la sesiones se pretende tomar datos sobre aspectos vinculados con el  impacto visual, estado de conservación de zonas de la visita, señalética, etc. El objetivo es aprovechar el potencial de RTCMapping para que los grupos de trabajo capturen los datos en tiempo real en sesiones de documentación en el mismo yacmiento arqueológico.

## Posilidades de RTCMapping.

Cuando el equipo de GeoWE me comentó ya hace unos meses la idea de desarrollar RTCMaping, no dudé sin duda en darles todo mi apoyo. Decidí, dentro de mis posibilidades, como usuario y profesional que trabaja con datos y aplicaciones geográficas, arrimar el hombro para que esta aplicación tenga todo el éxito que se merece. Toda persona interesada puede usar los canales habilitados (web, correo, [issues](https://github.com/geowe/RTCMapping)) para aportar su punto de vista, identificar errores o aportar comentarios.

![Sección de issues en el repositorio de GitHub](/images/blog/201807_rtcmapping/issues.png)

*Sección de issues en el repositorio de GitHub.*

Ya que mi trabajo últimamente está muy vinculado con urbanismo y ciudad, pienso en el potencial que RTCMapping tiene como **herramienta compartida de diseño urbano**.  Usando RTC podemos contar con un mismo tablero geográfico a escala real, donde los miembros de un equipo que por ejemplo estén vinculados al desarrollo de un plan urbanístico, puede trabajar sin la necesidad de estar en una misma oficina, en el diseño de un nuevo espacio urbano. 

![Capas base. Catastro y ortomágen](/images/blog/201807_rtcmapping/salamapeadoplanparcial.png)

*Ejemplo de sala con dos usuarios generando datos en tiempo real.*

Simplemente con poder dibujar sobre fotografías aéreas y Catastro, se abre un gran abanico de posibilidades para ese tipo de proyectos. Si a eso le sumamos la opción de enriquecer la información geográfica (parcelario, trazado de viales, localización de infraestructuras, análisis de acceso, análisis de usos actuales...) con datos alfanuméricos, RTCMapping tiene sin duda mucho que ofrecer en este campo.


Una vez terminada la sesión los datos generados pueden ser descargados y posteriormente tratados con otras aplicaciones de escritorio como un SIG o incluso un CAD.

![Datos de RTCMapping en QGIS](/images/blog/201807_rtcmapping/qgis.png)

Poco a poco van surgiendo nuevos ámbitos de aplicación (emergencias, tracking, monitorización…) y con toda seguridad, como en el caso de la toma de datos en Medina Azahara, las posibilidades serán muchas. 
