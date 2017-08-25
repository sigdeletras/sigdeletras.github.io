---
title:  "Trabajando con Spatialite"
excerpt_separator: "<!--more-->"
comments: true
related: true
categories: 
      - 2014
tags:
      - QGIS
      - Sistemas de Información Geográfica
      - Spatialite
---
        
Una de las características que más me atrae de lo SIG _open source_ es la capacidad de trabajar con gran variedad de formatos geográficos tanto de tipo archivo (shape, geojson, kml,csv o dxf) como en bases de datos geográficas (Postgres/PostGIS, MySQL o Geodatabase de ESRI).

Esta ventaja conlleva por otro lado un problema centrado en la elección del formato de almacenamiento según el tipo proyecto, encargo o trabajo SIG. Una buena entrada para comprender las ventajas/desventajas de cada sistema titulada**[Shapefiles vs bases de datos espaciales](http://mappinggis.com/2012/08/shapefiles-vs-bases-de-datos-espaciales/)** puede encontrarse en la web MappingGIS de Aurelio Morales.

En mi caso, cuando el proyecto GIS tiene

*   cierta entidad respecto al número de capas,
*   es necesario crear información geográfica combinado varias capas de datos mediante (views),
*   requiere campos de tipo texto exceden la capacidad de 254 caracteres o
*   se necesitan estilos gráficos prediseñados de visualización

mi decisión se decanta por el uso de una base de datos geográfica, normalmente **PostgreSQL/PostGIS**.

Como bien se indica en el trabajo **[Panorama del SIG Libre](https://panorama-sig-libre.readthedocs.org/es/latest/bbdd/index.html)** presentado en las 8ª Jornadas de SIG Libre, el uso de PostGIS dentro del sector GIS es fundamental y _"aunque su uso a nivel general no está tan extendido como MySQL, dentro del sector GIS su uso es casi canónico"_. Pero existen algunas ocasiones, sobre todo cuando el usuario/cliente no tiene los conocimientos suficientes para la instalación y administración de bases de datos tipo Postgres/PostGIS, el volumen de datos no requeire el despliegue de una infraestructura de gran tamaño o no es necesario el trabajo la edición simultánea de varios usuarios (concurrencia) donde PostgreSQL/PostGIS puede quedarnos un poco largo. En esos momentos es cuando entra en acción base de datos basada en ficheros **Spatialite**.

Spatialite es ua extensión que agrega a SQLite el soporte para datos espaciales según las especificaciones de la OGC. Podríamos decir que **Spatialite es a SQLite lo que PostGIS es a PostgreSQL**. La gran diferencia entre las dos sistemas de almacenamiento es que SQLite/Spatialite está configurado por un único fichero lo que facilita su "portabilidad" (no sé si es muy adecuado utilizar este adjetivo pero creo que se entiende) y es bastante sencillo de instalar y configurar. Para saber más sobre las funcionalidades principales de Spatialite se puede acceder a la [página oficial del proyecto Spatialite](http://www.gaia-gis.it/gaia-sins/)o a este enlace de la [documentación de OSGeoLive](http://live.osgeo.org/es/overview/spatialite_overview.html) sobre la extensión.

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-08-20-trabajando-con-spatialite.md#spatialite-para-rude-men)Spatialite para _rude men_

Tras obtener los archivos binarios desde la [página oficial](http://www.gaia-gis.it/gaia-sins/) e instalar según el sistema operativo (en mi caso con sudo apt-get install spatialite-bin), podemos trabajar con Spatialite desde la terminal usando el comando _spatialite_. A continuación tenéis un ejemplo de conexión

    spatialite /home/user/data/spatialite/equipamientos_culturales.sqlite

y otro de una consulta.

    SELECT ROWID, "Name", "tipologia", "geometry"FROM "equipamientos_culturales"WHERE "tipologia" = "Museos";
    
Si lo nuestro no es la consola o no somos unos verdaderos _rude men_ podemos instalar y utilizar la **interfaz gráfica****_spatialite_gui_**. Con esta herramienta podremos crear nuestras bases de datos, importar/exportar ficheros (shapes, csv/txt, dbf o xls), generar consultas, realizar operaciones geográficas, acceder a los metadatos de la base de datos o ver el historial de operaciones entre otras operaciones. Desde esta GUI podremos también obtener una vista geográfica simple de nuestros datos y salvarla a un formato gráfico como png, svg o pdf. Para la versión 1.5 existe un tutorial rápido en inglés en este [enlace](http://www.gaia-gis.it/gaia-sins/spatialite-gui-docs/spatialite_gui-1.5.0.pdf).

[![03_spatialite_gui](https://camo.githubusercontent.com/ff558accea4389444dd946b0e9af07c24a91fe90/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333837312f31343739323639383334385f326161376463373866615f7a2e6a7067)](https://camo.githubusercontent.com/ff558accea4389444dd946b0e9af07c24a91fe90/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333837312f31343739323639383334385f326161376463373866615f7a2e6a7067)

_Spatialite GUI_

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-08-20-trabajando-con-spatialite.md#trabajando-con-spatialite-con-qgis)Trabajando con Spatialite con QGIS

Para ponerlo aun más fácil, desde **QGIS** podremos trabajar, crear y editar sin problemas datos espaciales en Spatialite, ya que este SIG permite por defecto conectarnos a este tipo bases de datos geográficas. Los menús, operaciones y accesos más comunes son:

*   Creación de una nueva capa y su correspondiente fichero rápidamente desde el menú _Capa>Nueva>Nueva Capa Spatialite_
*   Añadir una capa desde una una bbdd ya existente desde _Capa>Añadir capa Spatialite_
*   Gestionar la base de datos desde el Administrador de Bases de datos del menú _Base de Datos_. Desde aquí podremos realizar algunas tareas administrativas como crear, borrar o renombrar capas o importar/exportar archivos.

[![06_administrador_bbdd](https://camo.githubusercontent.com/a91f340882cd5112f424df2ff457edd44c48ce7e/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333833372f31343739323631393133395f306261326139636664355f7a2e6a7067)](https://camo.githubusercontent.com/a91f340882cd5112f424df2ff457edd44c48ce7e/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333833372f31343739323631393133395f306261326139636664355f7a2e6a7067)

_Administrador de BBDD_

Podemos también trabajar con la **[extensión QSpatiaLite](https://code.google.com/p/qspatialite/)** que incluye muchas de las operaciones que podemos realizar desde _spatialite_gui_ pero sin salirnos de QGIS. Podemos crear sentencias SQL avanzadas o importar/exportar ficheros según los formatos espaciales OGR. En el siguiente ejemplo obtenemos una tabla con el número de equipamientos culturales por cada barrio del conjunto histórico de Córdoba.

    SELECT  "da04_barrio_ch".'barrio' , COUNT(*) FROM  "equipamientos_culturales" ,  "da04_barrio_ch"      WHERE  Within( "equipamientos_culturales".'geometry' ,  "da04_barrio_ch".'geom' ) GROUP BY   "da04_barrio_ch".'barrio';

[![08_qgis_QspatiaLite](https://camo.githubusercontent.com/c39d0a7f9b5768ca9ad29d912cda61159a6f8b9f/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333835322f31343935363331393239365f623839353030303739625f7a2e6a7067)](https://camo.githubusercontent.com/c39d0a7f9b5768ca9ad29d912cda61159a6f8b9f/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333835322f31343935363331393239365f623839353030303739625f7a2e6a7067)

_Extensión QSpatiaLite_

Por último, y no menos importante, la última versión de QGIS (2.4) permite **añadir a nuestra base de datos los estilos de visualización** y consulta de datos definidos para nuestras capas y asignarlos como estilos por defecto. Este opción es realimente interesante, ya que en un mismo fichero podemos incluir el aspectos gráficos de nuestras capas. Para guardar el estilo, accederemos a la pestaña _Estilo_ del formulario _Propiedades de la capa_. Tras definir el tipo de visualización, pincharemos el botón "Guardar estilo" y la opción "Guardar en base de datos (spatialite)"

[![09_qgis_salvar_estilo](https://camo.githubusercontent.com/25bffe657f1c1289ce37a529a18a932030579e60/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353537322f31343739323631393631395f366335336265633636635f7a2e6a7067)](https://camo.githubusercontent.com/25bffe657f1c1289ce37a529a18a932030579e60/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353537322f31343739323631393631395f366335336265633636635f7a2e6a7067)

_Guardar estilo en base de datos_
        