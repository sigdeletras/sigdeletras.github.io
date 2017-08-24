---
title:  "dxf2gmlcatastro. Script Python para convertir de DXF a GML parcela catastral"
excerpt_separator: "<!--more-->"
comments: true
header:
      teaser: "/images/header/2016-05-03-dxf2gmlcatastro.jpg"
related: true
categories:
      - Blog
tags:
      - Catastro
      - Python
      - Inspire
---

Estas últimas semanas conocidos y amigos que se dedican a la arquitectura, la tasación inmobiliaria me han hecho consultas sobre la generación del archivo GML que debe añadirse a la descripción grafíca que describe informáticamente las parcelas catastrales.

<!--more-->

Laboralmente no he tenido que realizar trabajos vinculados con Catastro, por para enterarme un poco de que iba el tema tuve que leer algunos documentos técnicos colgados en la web de la Dirección General de Catastro, blog especializados y algún que otro foro.

Según he podido, leer cuando la certificación catastral descriptiva y gráfica no coincide con la realidad es necesario elaborar una representación gráfica alternativa a la que se debe añadir un XML con contenido geográfico que no es otro que el famoso GML.

Este mismo archivo es también accesible, como adjunto, en las certificaciones catastrales descriptivas y gráficas, desde la consulta interactiva de un bien inmueble y desde servicios web WFS.

Mi primera respuesta a fue que se usara un SIG de escritorio para pasar el DFX al GML pero parece que no es tan sencilla el esquema no está disponible aún en la mayoría de los SIG (parece que en la última versión de gvSIG 2.3 está disponible). El formato de parcela catastral debe cumplir el estándar INSPIRE cadastral parcel definido en INSPIRE Data Specification on Cadastral Parcels - Guidelines version 3.0.1\. L

## ¿Cómo generar el GML?

La Dirección General del Catastro ha colgado de su web una serie de guías técnicas en las que se explica entre otros cómo generar un GML de Parcela Catastral. En el mismo apartado hay un par de ejemplos con explicaciones comentadas de archivos GML validados para parcela catastral y para edificio.

En la guía se definen los siguientes pasos:

*   Paso 1: Descarga de un fichero DXF de la sede electrónica del Catastro conteniendo la cartografía de la zona en la que se desea intervenir.
*   Paso 2: Edición del fichero con AUTOCAD (...u otro programa CAD o incluso SIG) y generación de un nuevo fichero DXF.
*   Paso 3: Modificación manual del fichero DXF generado y obtención de coordenadas.
*   Paso 4: Generación del fichero GML para adaptarlo al formato de parcela catastral.
*   Paso 5: Validación del fichero GML en la Sede Electrónica del Catastro.

Todo este proceso es bastante "artesano" y lo primero que se me ocurrió es que algunos de estos pasos (3 y 4) se podría automatizar con un poco de programación con el fin de ganar tiempo y evitar errores que se puedan generar por la edición manual. Tras algunas lectura y documentación pensé en generar un pequeño código en Python usando la librería GDAL y compartirlo en GitHub para que pueda ser utilizado y espero que mejorado.

## ¿Cómo funciona dxf2gmlcatastro.py?

### Descargar dxf2gmlcatastro

En primer lugar debemos descargar/descomprimir o hacer un _git clone_ de los archivos python disponibles en el repositorio [dxf2gmlcatastro en GitHub](https://github.com/sigdeletras/dxf2gmlcatastro).

### Instalar Python y la libraría GDAL.

En Ubuntu **Python** viene instalado por defecto. De todas formas si queremos comprobarlo y ver la versión instalada sólo hay que ejecutar desde terminal el siguiente comando

    $ python --version
    Python 2.7.6

La librería [GDAL](https://pypi.python.org/pypi/GDAL/) es la que se encargará de todas las operaciones de acceso y lectura del archivo DXF. Para usarla con Python he instalado _python-gdal_.

    $ sudo apt-get install python-gdal

Todo el trabajo se ha realizado en Ubuntu. Para [Windows](https://www.python.org/downloads/), tras instalar Python, podría utilizarse el administrador de paquetes Python [Pip](http://recursospython.com/guias-y-manuales/instalacion-y-utilizacion-de-pip-en-windows-linux-y-os-x/).

### Ejecutar dxf2gmlcatastro.py (v.2*)

* Agradecer al inestimable ayuda y PR de Marcos Ortega de [Indavelopers](http://www.indavelopers.com/ "indavelopers")

Desde la consola ejecutamos el comando _dxf2gmlcatastro.py_ indicando a continuación la ubicación del archivo DXF, el nombre del nuevo archivo GML y el código EPSG del Sistema de Referencia de Coordendas del archivo DXF.

    $ pyhon dxf2gmlcatastro.py archivocad.dxf archivogmlcatasro.gml 25830

Toda la información junto a archivos de ejemplo puede consultarse en el [repositorio GitHub](https://github.com/sigdeletras/dxf2gmlcatastro "Github").

## 2do

*   <span style="text-decoration: line-through;">Permitir elegir el SRC del GML.</span> (v.2)
*   Investigar qué es el "Identificativo local de la parcela" y se si debería solicitar al ejecutar el script.
*   <span style="text-decoration: line-through;">Poder elegir el archivo DXF a transformar.</span> (v.2)
*   <span style="text-decoration: line-through;">Poder elegir el archivo GML a crear.</span>(v.2)
*   Generar un GML de varias parcelas catastrales.
*   Crear un script para edificio.
*   Probarlo en otros Sistemas Operativos. (MacOS)
*   Probarlo en QGIS

## Referencias

*   [¿CÓMO GENERAR UN GML DE PARCELA CATASTRAL?. Direccion General de Catastro](http://www.catastro.minhap.es/documentos/portal%20generacion%20GML.pdf)
*   [Documentación técnica. Direccion General de Catastro](http://www.catastro.minhap.es/esp/CoordinacionCatastroRegistro.asp#doctec)
*   [GML parcela catastral: como generar un fichero de coordenadas GML válido para Catastro. Blog GESPASUR de Pedro E. Fuster Villa](http://gespasur.blogspot.com.es/2016/01/como-generar-un-fichero-de-coordenadas.html)
*   [Representación gráfica alternativa y formato GML en la georreferenciación de la propiedad inmobiliaria. Albireo Topografia](http://www.albireotopografia.es/representacion-grafica-alternativa-y-formato-gml-en-la-georreferenciacion-de-la-propiedad-inmobiliaria/)
        
