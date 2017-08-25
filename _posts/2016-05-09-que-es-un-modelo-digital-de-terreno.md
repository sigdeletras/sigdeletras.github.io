---
title:  "Qué es un Modelo Digital de Terreno"
excerpt_separator: "<!--more-->"
comments: true
header:
  teaser: "/images/header/2016-05-09-portada_mde.jpg"
related: true
categories: 
  - 2016
tags:
 - QGIS
 - Sistemas de Información Geográfica
 - Arqueología
 - MDT
---

Un **_Modelo Digital de Terreno (MDT)_** es una estructura numérica de datos que representa la distribución espacial de una variable cuantitativa y continua. El tipo de MDT más conocido es el **Modelo Digital de Elevaciones (MDE)**, un caso particular de aquel, en el que la variable representada es la cota del terreno en relación a un sistema de referencia concreto (Fuente:[Wikipedia](https://es.wikipedia.org/wiki/Modelo_digital_del_terreno)).

<!--more-->

Su campo uso es muy variado:

*   Extracción de los parámetros del terreno.
*   Trazados de perfiles topográficos.
*   Creación de mapas en relieve.
*   Tratamiento de visualizaciones en 3D.
*   Planificación de vuelos en 3D.
*   Creación de modelos físicos (incluyendo creación de mapas de relieve).
*   Rectificación geométrica de fotografías aéreas o de imágenes satélites.
*   Los análisis del terreno en geomorfología y geografía física.
*   Apoyo en análisis estadísticos (precipitación, insolación-temperatura, flujos hídricos, erosión, distribución de hábitats, etc.)
*   Modelos climáticos (sombras, incidencias del sol, umbrías)
*   Modelos hidrológicos (líneas de flujo,áreas subsidiarias, caudales)
*   Análisis visual

Para trabajos localizados en España, la fuente fundamental de Modelos Digitales de Elevación es el **Instituto Geográfico Naciona**l. Sus Modelos Digitales del Terreno se obtienen mediante interpolación de modelos digitales del terreno de 5 metros de paso de malla procedentes del Plan Nacional de Ortofotografía Aérea (PNOA). La **descarga de los datos** se realiza a través de la dirección [http://centrodedescargas.cnig.es/CentroDescargas/](http://centrodedescargas.cnig.es/CentroDescargas/)

 ![MDT de descarga en la web del CNIG](/images/blog/05_mde/mde_cnig.png "MDT de descarga en la web del CNIG")

<span style="font-size: small;">_MDT disponibles para descarga en la web del CNIG_</span>

Los Sistemas de Información Geográfica como **QGIS** incorporan un conjunto de herramientas que permiten realizar procesos de conversión, tratamiento y análisis de MDE. Entre las operaciones más frecuentes se encuentran:

*   Obtención de **curvas de nive**l en formato vectorial y si lo deseamos exportar estos datos a formato DXF para su trabajo con CAD.
*   Generación de p**erfiles longitudinales.**
*   **Visualización 3D**.
*   Generación de **mapas de sombras** que nos ayuden a una mejor comprensión de la topografía y el relieve existente sin la necesidad - de acudir a un mapa topográfico.
*   Mapas de **orientación**
*   Obtención de **mapas de pendientes** que son extensamente usados en trabajos de análisis arqueológico del territorio, sobre todo - como parte de cálculos de análisis de visibilidad, costo de desplazamiento o caminos óptimos.
*   La **reclasificación** es una operación matemática sobre archivos raster que permite generar nuevos valores a partir de determinados criterios y operaciones. Por ejemplo, al generar un mapa de pendientes en porcentajes tendremos para cada celda un valor comprendido entre 0 y 100.

![](/images/blog/05_mde/pendientes.png)

 <span style="font-size: small;">_Ejemplo de mapa usos posibles de suelo según pendiente_</span>

En el Curso online [“Sistemas de Información Geográfica y Arqueología"](http://www.almagre.es/cursos-formacion/curso-online-sistemas-de-informacion-geografica-qgis-y-arqueologia) se tratará con más amplitud las posibilidades que los MDT tienen en el campo de los análisis de territorio pasados y se obtendrán los conocimientos para el manejo de esta relevante fuente de información geográfica con el Sistema de Información Geográfica QGIS.        
