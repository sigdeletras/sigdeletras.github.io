---
title:  "Trabajando con coordendas geográficas GGMMSS con QGIS"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201901_coordenadasgms/1280px-TabulaRogeriana_upside-down.jpg" 
categories: 
  - 2019
tags:
  - qgis
---
Tener unos conocmientos básicos, pero claros, sobre [Geodesia](https://es.wikipedia.org/wiki/Geodesia) es una de las claves en las que se basa el uso profesional de los Sistemas de Información Geográfica. Son temas un tanto complicados, sobre todo para aquellas personas no vinculadas con carreras como la ingeniería geodésica, topografía o la geografía, pero pero por otro fundamentales. 

En los cursos que me ha tocado impartir, suelo añadir un pequeño anexo con explicacionenes sencillas de conceptos como: elipsoide, datum, proyecciones, latitud, longitud.... También recomiento este dossier titulado ["Concpetos de Cartografía"](http://www.ign.es/web/resources/cartografiaEnsenanza/conceptosCarto/descargas/Conceptos_Cartograficos_def.pdf) editado por el IGN o este [otro sobre Geodesia](http://www.ign.es/web/resources/docs/IGNCnig/GDS-Teoria-Geodesia.pdf), en esta ocasión un tanto más avanzado.

![The Tabula Rogeriana](/images/blog/201901_coordenadasgms/1280px-TabulaRogeriana_upside-down.jpg)
*The Tabula Rogeriana, drawn by Muhammad al-Idrisi for Roger II of Sicily in 1154. Wikipedia*

## Coordendas geográficas en notación sexagesimal

En esta ocasión, voy a comentar un caso específico que me ha pasado esta semana, en la que me tenido que crear una capa con la localización de las redes metereológicas del AEMET situadas en Andalucía. Quitando un formato un tanto estraño, según los metadatos las coordendas geográficas, la localziación de cada estación se ofrecía en en sistema sexagesimal por lo había que realziar trabajos de edición para poder incorporarlas a la base geográfica PostGIS del proyecto.

Las coordenadas de las casis 2000 estaciones, como comento se encuentran en notación sexagesimal, o lo que es lo mismo representadas en grados, minutos y segundos. Las partes de grado inferiores al segundo se expresan como parte decimal de segundo.  A este sistema se le añade las siglas N/S para la latitud según hemisferio en que nos encontremos y E/W en la longitud según su situación en relación Meridiano de Greenwich. 

Un ejemplo de coordenada en este sistema sería:

```
Latitud: 41º 39' 24,08" N
Longitud: 0º 52' 43,14" W
```
![Señal indicativa del paso del meridiano de Greenwich (ED-50) sobre la autopista AP-2 en las inmediaciones de Fraga (Huesca-España)](/images/blog/201901_coordenadasgms/Meridiano_0(AP-2)(Señal).jpg)
*Señal indicativa del paso del meridiano de Greenwich sobre la autopista AP-2 en las inmediaciones de Fraga (Huesca-España). Wikipedia*

Este formato de representación no es sin embargo el más usado dentro de los SIG. Es más comín trabajar con datos en sistemas de coordenadas geográficas (WGS84, ETRS89…) pero con notación decimal. En este caso las latitudes 0° y 90 ° correspondería al Hemisferio Norte y las que se encuentra entre 0° y -90° al Hemisferio Sur. Para la Longitud, los valores entre 0° y 180° se sitúan al Este del meridiano de Greenwich y los grados entre 0° y -180° son situaciones al Oeste de dicho meridiano. Así las coordenadas anteriores, en sistema decimal corresponderían con:

```
Latitud: 41,6566895775
Longitud: -0,8786487579
```
Existen varias aplicaciones on-line que permiten realizar la conversión entre los dos sistemas, aunque la transformación podría realizarse generando los cálculos en una simple hoja de cálculo. 

Un ejemplo de esto la ofrece el mismo Instituto Geográfico Nacional. Accediendo a la siguiente URL http://www.ign.es/web/gds-web-srv-coord  se abre una  aplicación web que permite transformar las coordenadas de un punto o un conjunto de datos en formato GML de un sistema de referencia a otro mediante un servicio WPS . Este servicio soporta los datum ETRS89 y ED50, en coordenadas geográficas y en coordenadas planas.

## Generando una capa de puntos a partir de coordenadas GGMMSS con QGIS 3

Si tenemos un listado de coordenadas en formato GGMMSS, podemos usar la opción **“Añadir capa de texto delimitado” de QGIS** para generar una capa geográfica con estos datos.

La única condición es que en los pares de coordenadas GGMMSS deben sustituirse los simbolos de grados (º), minutos (') y segundos('') por espacios y los caracteres N/S y E/W deben colocarse inmediatamente despues de los minutos. Este cambio se podría hacer con cualquier editor de texto.

Así las coordendas del ejemplo quedaría así:

```
Latitud: 41 39 24,08 N
Longitud: 0 2 43 14W
```
Supongamos que tenemos un listado de coordenadas previamente tratado para que se ajuste a este formato:

![Lista](/images/blog/201901_coordenadasgms/lista.png)

- Abrimos QGIS y accedemos al menú **Capa>Añadir capas>Añadir capa de texto delimitado**
- Cargamos nuestro archivo delimitado. Por ejemplo un CSV.
- A continuación, vamos eligiendo los parámetros de configuración según el fichero. En este caso, el separador de decimales es la coma por lo que hay que indicarlo.
- Los campos de coordenadas con el formato coorecto son *longQGIS* (Campo X) y *latitudQGIS* (Campo Y).
- Y aquí viene la clave: **debemos marcar la casilla “Coordenada GMS” para que el sistema nos reconozca el formato GGMMSS.**
- No se nos puede olvidar indicar el SRC de los datos. Para el ejemplo es EPSG: 4258 - ETRS89.

![Carga capa QGIS](/images/blog/201901_coordenadasgms/qgis.png)

Aceptando las opciones, y si hemos elegido nuestros parámetros correctamente tendremos disponible nuestra capa en QGIS. Si lo deseamos podemos exportar los datos a una capa geográfica, o incluso reproyectarla a coordenadas planas.
