---
title:  "Curso QGIS Avanzado con la Asociación Geoinnova"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201910_cursogeoinnova/portada.png" 
categories: 
  - 2019
tags:
  - Formación
  - QGIS
---


El próximo 15 de octubre tendré el placer de tutorizar el curso "**QGIS Avanzado. Herramientas avanzadas** organizado por la [Asociación Geoinnova.](https://geoinnova.org/) Geoinnova es una entidad compuesta por amplio equipo de profesionales y que está especializada en la consultoría ambiental y la formación dentro del ámbito geoespacial.

![html](/images/blog/201910_cursogeoinnova/GEOINNOVA.png)

Este curso supone para mi una magnífica oportunidad para poder trasladar a los alumnos que se matriculen, la experiencia acumulada como geógrafo profesional y formador en Sistemas de Información Geográfica, en concreto del conocido SIG de escritorio de código abierto [QGIS](https://www.qgis.org/es/site/).

![QGIS 3.8](/images/blog/201910_cursogeoinnova/qgis318.png)

Junto al equipo de Geoinnova he preparado un temario pensado en la adquisición de conocimientos y habilidades para usuarios y profesionales que ya posean cierta experiencia en el uso de QGIS pero que quieren mejorar la explotación de esta potente herramienta.

En un primer bloque se tratarán temas relacionados con la configuración avanzada de QGIS (opciones, manejo de capas, archivos de definición, acciones...) sobre su **última versión QGIS 3.8 Zanzibar**. Se puede consultar en la siguiente en la hoja de ruta de la documentación oficial la relación de [novedades de esta última versión](http://changelog.qgis.org/en/qgis/version/3.8/) denominada así por la ubicación la reunión de desarrolladores del proyecto en 2018.

Tras esta primera unidad, nos centraremos en el manejo de datos vectoriales. En el tema se explicarán aspectos del SIG para la **gestión de datos alfanuméricos, las consultas mediante expresiones, la personalización de formularios y la obtención de estadísticas** sobre los mismos. Siguiendo con la información en modelo vectorial, veremos herramientas para **edición profesional** de este tipo de geometrías, así como la creación de capas de datos a partir de geoprocesos espaciales y usando expresiones. Pienso que también será de interés aprender a enriquecer nuestras capas con la unión de conjuntos de datos externos. 

El bloque vectorial termina con una unidad dedicada a la **topología**. Haremos una explicación teórica que mostrará los principales **tipos de errores topológicos** y veremos como podemos identificarlos gracias al *pluging* de topología de QGIS. Para finalizar, los alumnos aprenderán **técnicas de depuración** de errores mediante geoprocesos con la función v.clean de GRASS.

![Topología](/images/blog/201910_cursogeoinnova/topologia.png)
*Análisis de topología en QGIS*

Cuando manejamos cierto volumen de datos y trabajamos de forma corporativa con ellos, es importante el almacenamiento y gestión de los mismos en bases de datos geográficas. Como no podría ser de otra forma, veremos las posibilidades que nos ofrece el sistema de gestión de bases de datos relacional **PostgreSQL junto a la extensión espacial PostGIS**. En las prácticas guiadas se aprenderá cómo instalar y configurar este sistema, el uso de la aplicación gráfica **pgAdmin4** y el manejo de **SQL** como lenguaje de gestión de bases de datos relacionales. Aplicaremos los conocimientos adquiridos para conectarnos y realizar consultas a nuestra base de datos geográfica desde QGIS.

Una vez que hayamos aprendido a manejar PostGIS, seguiremos con una unidad específica destinada al **análisis de redes (grafos)**. QGIS cuenta con un importante conjunto de procesos destinados a este tipo de análisis. Junto a las herramientas propias de QGIS, se aprenderá a crear y analizar los datos de una red con la potente extensión de PostgreSQL [pgRouting](https://pgrouting.org) orientada al trabajo con rutas y que permite el cálculo de caminos óptimos basados en distancia, tiempo, coste.

![red](/images/blog/201910_cursogeoinnova/red.png)
*Red por distancia*

En la programación se ha incluido un apartado dedicado al **manejo avanzado de simbología y etiquetado** (basada en reglas, diagramas,  contornos estilo Tanaka o simbología por tamaño)** y la **presentación de salidas gráficas e informes con  Atlas**. El uso de expresiones y de texto HTML enriquecido dentro de nuestro diseño de mapas permitirá la creación optimizada de presentaciones profesionales.

![atlas](/images/blog/201910_cursogeoinnova/atlas.png)
*Composión con Atlas con análisis ráster y 3D*

Tres de los temas del curso van a centrarse en la **explotación de datos ráster**. En uno de ellos, trabajaremos en profundidad con **modelos digitales del terreno**, realizando distintos procesos como **análisis de pendientes, impacto visual o extracción de curvas de nivel**. Gracias las últimas mejoras en QGIS explotaremos las posibilidades que la **visualización 3D de MDE** nos ofrece. En la siguiente unidad se tratarán tanto geoproceosos avanzados orientados a datos ráster como la aplicación la generación de **estadísticas zonales, reclasificaciones**, terminando manejo básico de **datos multiespectrales y cálculo de distintos índices (NDVI, NDWI, NDSI...)**. 

Este bloque temático se cerrara con el **trabajo de datos LiDAR**. La unidad comenzará con la instalación de LAStools en QGIS, gracias a la cual podremos visualizar datos en dos y tres dimensiones. Los datos LiDAR recopilan gran cantidad de datos que pueden ser clasificados según el objetivo de nuestro análisis. Para finalizar usaremos varios procesos con LAStools que permitirán por ejemplo la detección de bordes de edificaciones, la identificación de masas de vegetación y la generación de perfiles.

![lidar](/images/blog/201910_cursogeoinnova/lidar.png)
*Trabajo de detección de bordes sobre datos Lidar y perfil de edificación.*

He querido añadir un tema dedicado al conocimiento del **Modelador gráfico de procesos de QGIS**. La parte práctica está enfocada como un proyecto profesional de uso de los SIG en que el que definirán distintos procesos para el análisis desarrollados en un modelo totalmente configurable.

Pero este curso de QGIS avanzado no podría terminar sin incluir una **última unidad orientada a la difusión de datos espaciales en Internet**. Tras una introducción al desarrollo web basados en sus principales lenguajes de programación (HTML, CSS y JavaScript) usaremos un conjunto de complementos de QGIS (**QGIS2WEB**) para la creación de visores de mapas desde nuestro SIG de escritorio.

Toda la información del curso de **QGIS Avanzado** (objetivos, destinatarios, precio y plazos de matriculación) pude consultarse en la [página de la Asociación Geoinnova](https://geoinnova.org/cursos/curso-qgis-avanzado-online-certificado/), a la que desde aquí quiero agradecer que cuente conmigo para esta acción formativa.

