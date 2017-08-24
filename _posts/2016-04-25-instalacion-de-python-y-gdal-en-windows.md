---
title:  "Instalación de Python y GDAL en Windows"
excerpt_separator: "<!--more-->"
comments: true
header:
  teaser: "/images/blog/01.png"
related: true
categories: 
- Blog
tags:
- Catastro
- Python
- GDAL
---

Dentro del programa de la [11ª reunión de Geoinquietos Córdoba](http://wiki.osgeo.org/wiki/Reuni%C3%B3n_11_Geoinquietos_C%C3%B3rdoba) voy a realizar de mini taller donde explicar cómo se usa el script Pyhton [**dxf2gmlcatastro**](https://github.com/sigdeletras/dxf2gmlcatastro) que estoy generando para convertir un archivo CAD DXF al formato GML definido por tras la [Resolución conjunta Catastro-Registro](http://www.catastro.minhap.es/documentos/formatos_intercambio/Formato%20GML%20parcela%20catastral.pdf).

<!--more-->

Desde hace unos meses he empezado a aprender Python y su aplicación temas geo. Este ejercicio de programación me está sirviendo bastante para ir adquiriendo los conocimientos básicos de este lenguaje. Además de las lecturas y pruebas, la ayuda de Marcos Ortega de [Indavelopers](http://www.indavelopers.com/) está siendo crucial.

Un rápido sondeo ha puesto de manifiesto que la mayoría de las personas que asistente a las reuniones de geoinquietos usan Windows. Aunque todo la programación está hecha en Linux (Ubuntu), he montado una máquina virtual con Virtual Box para ver los pasos a dar para poder ejecutar el script en este sistema operativo. Existe una manera más rápida de configurar GDAL para Python que es instalando OSGeo4W y usar la _shell_ incorporada. Pero como siempre es un buen momento para aprender he decido tomar el camino más largo y aprovechar para escribir esta entrada.

## Instalación de Python

Para instalar Python es necesario entrar en el apartado de descargas de la página de [Pyhton](https://www.python.org/downloads/windows/)) y bajarse la versión del lenguaje que se quiera instalar según el sistema operativo. Para esta guía hemos utilizado _Python 3.4.4 - 2015-12-21 Windows x86 MSI installer_.

Una vez descargada, ejecutamos el archivo e instalamos según la configuración por defecto. El único aspecto al que en principio hay que atender es a marcar, si no lo está, la casilla que añade python.exe a nuestro PATH.

![](/images/blog/01.png)

Terminada la instalación, accedemos a _Sistema>Configuración avanzada del sistema_ y pinchamos en el botón _Variables del entorno_. Desde aquí, podemos comprobar que se ha añadido la ruta a la carpeta de Python, en nuestro caso "C:\Python34", para la variable PATH. Editamos esta variable y añadimos también las rutas C:\Python34\Lib\site-packages\ y C:\Python34\Scripts.

## Instalación de GDAL

Para poder usar la biblioteca geoespacial [GDAL](https://es.wikipedia.org/wiki/GDAL) con Python es necesario tener instalados los binarios con anterioridad. Esta parte de la entrada recoge la guía en inglés del siguiente [enlace](http://sandbox.idre.ucla.edu/sandbox/tutorials/installing-gdal-for-windows).

Lo primero es saber la versión del compilador que estamos utilizando. Para ello buscamos en nuestros programas IDLE (Python GUI) dentro de la carpeta de Python y lo ejecutamos. En la información de inicial podemos apreciar la versión del compilador (MSC v.1600). En este mismo texto obtendremos la arquitectura de nuestra máquina (32 o 64 bits).

![](/images/blog/02_ilde.png)

Recopilados estos datos, entramos en la web [www.gisinternals.com](http://www.gisinternals.com/release.php) para acceder a los archivos de GDAL según nuestra configuración (ej. release-1600-gdal-1-11-3-mapserver-6-4-2). Una vez en la página de descarga, localizaremos el enlace del core de GDAL (Generic installer for the GDAL core components), descargamos e instalamos. Para nuestro equipo el archivo descargado ha sido _gdal-111-1600-core.msi_

Tras la instalación, tendremos que volver a editar de nuevo las variables del entorno y añadiremos a PATH, precedida de punto y coma, la dirección de la carpeta de GDAL de nuestro equipo (ej. ;C:\Program Files (x86)\GDAL).

A continuación debemos añadir dos variables nuevas:

*   GDAL_DATA que apunte a la carpeta gdal-data (C:\Program Files (x86)\GDAL\gdal-data)
*   GDAL_DRIVER_PATH que apunte a la carpeta gdalplugins (C:\Program Files (x86)\GDAL\gdalplugins)

Para comprobar que hemos realizado correctamente la instalación accederemos al Símbolo del sistema como administrador y escribiremos _gdalinfo --version_. Si todo es correcto obtrendremos la versión de GDAL instalada

![](/images/blog/03_gdalinfo.png)

## Instalación de Python _bindings_

Para poder utilizar GDAL con Python vamos a instalar los _bindings_ que se encuentran en la misma web que hemos descargado los archivos binarios de GDAL. Un _binding_ es una adaptación de una biblioteca para ser usada en un lenguaje de programación distinto de aquel en el que ha sido escrita.

Como partimos de una instalación de Python 3, descagaremos e instalamos el archivo _GDAL-1.11.3.win32-py3.3.msi_

Para terminar, vamos a acceder de nuevo la GUI de Python IDLE y escribiremos el siguiente código importando GDAL en Python

```python
import gdal

```

Si no nos devuelve ningún mensaje de error, hemos terminado nuestra instalación.

Si queréis empezar trastear con Python y GDAL os recomiendo seguir los ejemplos de [Python GDAL/OGR Cookbook.](https://pcjericks.github.io/py-gdalogr-cookbook/index.html). También puede puede revisar el curso ["Geoprocessing with Python using Open Source GIS"](http://www.gis.usu.edu/%7Echrisg/python) de la Utah State University.
        
