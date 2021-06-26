---
title:  "Desinstalación de OSGeo4W… e instalación de la versión 2 de OSGeo4W"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202106_osgeo4w/00_osgeo4w-logo.png" 
categories: 
  - 2021
tags:
  - qgis
  - osgeo4w
---

[OSGeo4W]( https://trac.osgeo.org/OSGeo4W/) es un instalador para el sistema operativo Windows mantenido por la [Open Source Geospatial Foundation](https://www.osgeo.org/) que permite, entre otras cuestiones, tener una gestión avanzada de la instalación del Sistema de Información Geográfica de Código Abierto QGIS.

Además de QGIS, el programa permite la instalación de los SIG GRASS y SAGA, la librería GDAL/OGR y más de [150 paquetes geomáticos]( https://trac.osgeo.org/OSGeo4W/wiki/PackageListing).

![IMG OSGeo4W](/images/blog/202106_osgeo4w/00_osgeo4w-logo.png)

En mi caso, utilizo OSGeo4W para instalar QGIS porque me permite contar con versiones concretas de QGIS tanto de su lanzamiento RC (Release Candidate) como LTR (Long Term Release). 

En el trabajo tenemos desarrollos para clientes en distintas versiones, damos formación avanzada de QGIS basadas en las versiones estables y siempre es interesante ir revisando las novedades de los últimos lanzamientos.

## Problemas al instalar QGIS 3.20

El pasado 22 de junio, si abrió a la comunidad la versión [QGIS 3.20](https://www.qgis.org/en/site/forusers/visualchangelog320/index.html) y me dispuse a instalarla para comenzar a probar las nuevas funcionalidades. 

Al lanzar el Setup de OSGeo4W, con la opción avanzada de instalación, e intentar actualizar la versión de QGIS de la 3.18 a la 3.20, cuál fue mi sorpresa 😮 de que esta opción no estaba disponible.

![QGIS 3.20](/images/blog/202106_osgeo4w/qgis320.jpg)

En este momento recorde que en el grupo de Telegram de usuarios de QGIS España, se había comentado que existía una nueva versión de OSGeo4W. 

Efectivamente, al entrar en la página de descargas de QGIS (https://www.qgis.org/es/site/forusers/download.html) hay un aviso sobre este tema. En el texto se comenta que existe una nueva versión (OSGeo4W v2) y que requiere dependencias que no se encuentran en el nuevo instalador. Se recomiendo una instalación limpia o usar un directorio diferente.
IMG aviso QGIS

Perfecto entonces. Mi opción fue la de descargar la versión nueva e instalarla en un nuevo repositorio. Pero aquí comenzaron los problemas. Siguiendo los pasos normales de instalación empezaron a surgir gran cantidad de errores, surgidos seguramente por la incompatibilidad entre los paquetes, por lo que esta opción no llegó a buen puerto.
Quedaba optar entonces por la segunda opción. Desinstalación de OSGeo4W y de QGIS. Pero... sorpresa, OSGeo4W no cuenta con un desinstalador.

![Instalación avanzada con el setup de OSGEO4W](/images/blog/202106_osgeo4w/01_instalación_avanzada_setup.jpg)

## Desinstalando OSGeo4W

Parece que suele ser una pregunta recurrente ya que la misma página de OSGeo incluye en sus FAQ la respuesta a [cómo podemos desinstalar un paquete del instalador o el mismo desinstalador]( https://trac.osgeo.org/OSGeo4W/wiki/FAQ#IsthereawayofuninstallingpackagesorallofOSGeo4W).

![OSGEO4W versión 2](/images/blog/202106_osgeo4w/03_uninstatl.jpg)

Ya que nuestro objetivo era borrar por completo la antigua versión del setup y todos los paquetes instalados  la única opción que nos da es *"just delete the whole OSGeo4W file tree (usually C:\OSGeo4W)"* 😱

![OSGEO4W versión 2](/images/blog/202106_osgeo4w/02_osgeo4w_v2.jpg)

Como sabemos, este tipo de desinstalación puede darnos algunos problemas. Pero tras alguna que otra consulta expongo a continuación los pasos a dar y que en mi caso ha llegado a buen puerto la instalación.

###  1. Copia de la carpeta de perfiles

Cuando estamos trabajando **con QGIS toda la configuración personalizada del programa**, las conexiones a bases de datos y servicios OGC, simbología personalizada o incluso los complementos que tengamos instalados quedan **vinculados a un perfil**.

Esto significa que podemos crear tantas configuraciones personalizadas como deseemos. Por poner un ejemplo, recientemente desarrollamos un [complemento para la descarga del Catastro de la Comunidad Foral de Navarra]( https://geoinnova.org/blog-territorio/plugin-qgis-descarga-cartografia-catastral-navarra-geoinnova/). El complemento estaba en varios idiomas y para probar que se cargaban correctamente la traducción, generé un nuevo perfil con el euskera como idioma por defecto.

Lo primero que debemos hacer por tanto es realizar una copia de la carpeta profile que se encuentra en *C:\Users\[nombreusuario]\AppData\Roaming\QGIS\QGIS3*

Si queremos hacer una instalación limpia podemos borrar esta carpeta, tras realizar una copia de seguridad. Tras la instalación recuperaremos los perfiles que nos sean de interés.

### 2. Eliminación de carpetas y accesos directos

El siguiente listado recopila las carpetas que he tenido que borrar.

Carpeta raiz de OSGeo4W

- *C:\OSGeo4W64*

Carpetas de accesos directos

- *C:\ProgramData\Microsoft\Windows\Start Menu\Programs\OSGeo4W*
- *C:\Users\[nombreusuario]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\OSGeo4W*

Carpetas de perfiles (opcional)

- *C:\Users\[nombreusuario]\AppData\Local\QGIS*
- *C:\Users\[nombreusuario]\AppData\Roaming\QGIS\*

### 3. Limpieza del registro de Windows

Como último paso, es interesante pasar algún programa que nos limpie el registro de Windows. He usado la versión portable del clásico CCleaner.

## Instalando QGIS con OSGeo4W versión 2

Tenemos ahora el equipo preparado para la nueva instalación de la última versión de OSGeo4W.

Una vez descargada la versión 2 desde la página de QGIS, vamos siguiendo los pasos por defecto de la instalación avanzada. 

Como he comentado al principio, me interesa tener instalados los siguientes paquetes:

- QGIS LTR (3.16)
- QGIS RC (3.20)
- Plugins de GRASS para QGIS (para ambas versiones)

Marco estas opciones y comienza la instalación.

![Instalación de QGIS](/images/blog/202106_osgeo4w/04_instalacion.jpg)

Tras finalizar el proceso de instalación conseguí tener las versiones de QGIS deseadas en mi equipo y listas para poder seguir dando caña a mi SIG de cabecera.

<iframe src="https://giphy.com/embed/xT0GqssRweIhlz209i" width="480" height="320" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/breaking-bad-bryan-cranston-i-won-xT0GqssRweIhlz209i">via GIPHY</a></p>


