---
title:  "Charla Introducción a D3 geo en GeoDevelopers"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202105_d3_geodevelopers/slides.png" 
categories: 
  - 2021
tags:
  - qgis
  - informes
---

GeoDevelopers es una comunidad centrada en los desarrolladores o profesionales del ámbito SIG. Desde el 2015 organiza charlas y talleres sobre tecnologías geoespaciales. Estos eventos cumplen la doble labor: difundir tendencias, habilidades y conocimientos sobre temática vinculada con los Tecnologías de Información Geográfica y dar visibilidad a los geodevelopers de la comunidad.

Además de las citas, desde su página web [https://www.geodevelopers.org/](https://www.geodevelopers.org/) se pueden acceder a un repositorio de contenidos y código, lista de correos y videos y presentaciones de su canal de YouTube...

El último "invento" de [Raúl Jiménez]((https://www.linkedin.com/in/jimenezortegaraul/?locale=es_ES)) y [Liber Chapinal]((https://www.linkedin.com/in/libertadchapinalcervantes/)) , responsable de la comunidad, es un espacio coworking virtual abierto en Discord. Este geocowork está pensado para mejorar la experiencia del teletrabajo, poder socializar durante momento de pausa y ayudar a conocer a personas nuevas con intereses comunes. Hay una [página de FAQS](https://github.com/Geo-Developers/organization/blob/master/coworking.md#preguntas-frecuentes-acerca-del-coworking ) con toda la información.

Esta es mi segunda colaboración en GeoDevelopers. La primera vez Raúl me invitó a hablar sobre mi experiencia en el campo de las geotecnologías y hablé también de mi proyecto de fin de ciclo en el que desarrollé un [visor web de rutas turísticas usando Node y API Rest](http://sigdeletras.com/2020/presentacion-proyecto-fp-web-rutas-turisticas-node/). 

En esta ocasión, la temática de la charla se centró  en la librería **D3.js** y su uso para desarrollar visualizaciones basadas en datos geográficos. La charla tuvo un nivel introductorio, que es en el que yo me encuentro ahora mismo. El objetivo principal ha sido hacer un repaso a temas y conceptos que para mí han sido claves para poder comenzar a usar la librería D3. 

![Presentación](/images/blog/202105_d3_geodevelopers/slides.png)


El manejo y programación con las funciones geográficas de [D3-geo](https://github.com/d3/d3-geo)  es muy diferente al de las bibliotecas JavaScript de mapas más conocidas como Leaflet y OpenLayers. Debemos tener en cuenta su sintaxis, que recuerda a JQuery, como realizar la transformación de datos geográficos (GeoJSON) en paths de SVG, las opciones que ofrece el formato [TopoJSON](https://github.com/topojson/topojson), la aplicación de las proyecciones cartográficas o la forma en la que D3 crea elementos SVG con sus correspondientes atributos.

La segunda parte práctica del taller consistió en ir montando una visualización de datos geográficos con D3. El resultado sería un mapa temático con los datos del padrón de habitantes por municipios de Andalucía. El ejercicio se basa en dos entradas del blog sobre D3 pero subiendo un poco de nivel.

Hacía tiempo que no preparaba un taller de este tipo. La pandemia y el confinamiento ha hecho que la mayoría de las actividades presenciales en Córdoba hayan quedado en stand-by. Es por ello por lo que ha hecho mucha ilusión  preparar esta charla en Geodevelopers. Preparar un taller de este tipo y que todo salga bien me requiere sin duda un esfuerzo y dedicación. A pesar de esto,  preparar una charla siempre me aporta beneficios. Estos eventos son una magnífica experiencia para seguir aprendiendo y adquirir nuevas habilidades. 

Por poner algún "pero" al taller... una verdadera pena poder haber terminado el evento con unas geobirras 🍻 de las de codo en la barra. Pero tengo esperanza en que todo llegará.

Los datos finales del taller se encuentran disponibles en este [repositorio de GitHub](https://github.com/sigdeletras/d3-geom-geodevelopers)

En el canal de GeoDevelopers está la grabación de la charla.

<iframe width="560" height="315" src="https://www.youtube.com/embed/XrLQIV9dRiY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

