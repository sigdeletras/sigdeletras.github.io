---
title:  "Cómo usar módulos de Python en QGIS. Un ejemplo con dxf2gmlcatastro"
excerpt_separator: "<!--more-->"
header:
  teaser: "/images/header/2016-05-03-portada.jpg"
related: true
categories: 
   - Blog
tags:
   - Catastro
   - Python
   - GDAL
   - QGIS
---

Como he venido comentando en las dos últimas entradas, en el repositorio de GitHub de SIGdeletras podéis encontrar el script [**dxf2gmlcatastro**](https://github.com/sigdeletras/dxf2gmlcatastro) permite transformar un archivo de parcela catastral CAD con extensión DXF al formato GML establecido por Catastro para conseguir su validación gráfica en la Sede Electrónica del Catastro.
<!--more-->
Tras verlo con algunos compañeros, presentarlo en las última reunión de [Geoinquietos Córdoba](http://wiki.osgeo.org/wiki/Reuni%C3%B3n_11_Geoinquietos_C%C3%B3rdoba) y recibir varios correos de personas interesadas en usarlo, la conclusión a la que he llegado es la de que por muy útil que sea una herramienta **si la gente no sabe utilizarla ya se está perdiendo el sentido básico que motiva su creación.**

En esta línea, y poco después de publicar el _script_, [Óscar Martínez de MásqueSIG](https://twitter.com/masquesig?lang=es "Twitter de másquesig") escribió una estupenda entrada en la que explicaba [cómo usar dxf2gmlcatastro en gvSIG](https://masquesig.com/2016/03/16/script-para-convertir-dxf-a-gml-con-gvsig-2-3-gracias-a-sigdeletras/). Siguiendo las reflexiones de Óscar, podemos decir que integrar código en un SIG como gvSIG, o en nuestro caso [QGIS](http://www.qgis.org/en/site/), permite:

*   Al poder integrar el código en un SIG que trabaja con Python y GDAL, el uso inicial de la librería es más fácil.
*   No estamos limitados a la instalación en un [sistema operativo concreto](2016/instalacion-de-python-y-gdal-en-windows) ya tanto gvSIG como QGIS son SIG multiplataforma.
*   Podemos mejorarlo usando las funcionalidades que nos ofrece el propio SIG (cuadros de dialogo, interfaz visual...).
*   Se podría integrar en la barra de herramientas o incluso convertirlo en una extensión.

En conclusión y como dice Óscar …**”que pueda llegar a más gente, que al final es para lo que lo hacemos”.**

## Definir la variable PYTHONPATH

La variable PYTHONPATH es utilizada en QGIS para acceder a los módulos de Python. Esta variable ya se define durante la instalación apuntando a una carpeta denominada Python dentro del directorio de instalación del programa, o en la carpeta _.qgis2_ en Linux. A pesar de ello, vamos a añadir una ruta nueva más accesible donde vamos a guardar nuestro módulo.

Los pasos a seguir son los siguientes:

*   Abrir QGIS.
*   Ir al menú _Configuración>Opciones.
*   En la pestaña _Sistema_, buscamos el apartado _Entorno._
*   Activamos la opción _“Usar variables personalizadas…”
*   Pinchamos en el botón _“Añadir”_ y definimos la variable con las siguientes opciones:
    *   Aplicar: “Poner a continuación”
    *   Variable: PYTHONPATH
    *   Valor: Carpeta donde vamos a guardar nuestros archivos Python (ej. C:\scriptsqgis)
*   Pinchamos en _Aceptar_ y reiniciamos QGIS.

 ![](/images//blog/05_importarmodulo/01_pythonpath.png)

## Usar dxf2gmlcatastro en QGIS.

Lo primero que debemos hacer es descarga el código, o hacer un _git clone, _ de dxf2gmlcatastro desde el [repositorio de GitHub](https://github.com/sigdeletras/dxf2gmlcatastro) y copiar los archivos en la carpeta definida en PYTHONPATH (ej. C:\scriptsQGIS).

![](/images//blog/05_importarmodulo/02_1_github.png)

Lo primero es comprobar que QGIS accede a la nueva ruta que hemos añadido a PYTHONPATH. Una vez ejecutado de nuevo QGIS,  vamos a abrir la consola de Python integrada (_Complementos > Consola de Python)_ y escribimos _import dxf2gmlcatastro_ y después pulsamos "Intro". Si hemos seguido correctamente los pasos anteriores no nos debería devolver ningún error.

![](/images//blog/05_importarmodulo/02_consola.png)

A continuación vamos a ejecutar la función _crea_gml_ de dxf2gmlcatastro que convertirá nuestro archivo DXF al GML de Catastro. Dentro de la función tendremos de añadir los argumentos que nos indiquen:

*   Dónde se encuentra el archivo DXF (ej. 'C:\carpeta\archivoparcela.dxf')
*   El lugar y el nombre del GML(ej. 'C:\carpeta\gmlcatastro.gml')
*   El código EPSG del Sistema de Referencia de Coordenadas del DXF. (Los SRC admitidos son 25828, 25829, 25830 y 25831)

```
dxf2gmlcatastro.crea_gml('C:\carpeta\archivoparcela.dxf', 'C:\carpeta\gmlcatastro.gml', '25830')

```

Si todo ha ido correcto podemos cargar el nuevo GML en QGIS y comprobar que se ha generado correctamente y que incluye los atributos según el modelo de Inspire.

![](/images//blog/05_importarmodulo/04_qgis.png)

## Crear un script con PyQGIS personalizado

Una vez que disponemos de _dxf2gmlcatastro_ podemos crear otros fragmentos de código para integrarlo en QGIS. Aquí os dejo un ejemplo que carga el GML en QGIS.

Para crear este archivo hemos usado el editor de código de QGIS y una vez terminado lo hemos salvado en nuestro equipo con el nombre _catastroQGIS.py_. Sólo deberemos cargar el archivo en el terminal de Python de QGIS y cambiar la ruta y nombre de los archivos para utilizarlo cada vez que queramos.

![](/images//blog/05_importarmodulo/03_pyqgis.png)
El archivo _catastroQGIS.py_ se encuentra en la [carpeta _ejemplo_ del repositorio GitHub](https://github.com/sigdeletras/dxf2gmlcatastro/blob/master/ejemplo/catastroqgis.py "Ejemplo para QGIS")
        
