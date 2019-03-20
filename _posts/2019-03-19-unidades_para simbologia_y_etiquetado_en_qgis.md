---
title:  "Unidades para simbología y etiquetado en QGIS 3"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201903_unidades/portada.png" 
categories: 
  - 2019
tags:
  - QGIS
---

Adaptando los materiales sobre diseño de impresiones de los [cursos que imparto](http://www.sigdeletras.com/formacion/) con QGIS, pude comprobar que en la nueva versión había sido añadida la opción "Metros a escala" dentro del tipo de unidades a aplicar a las simbologías y etiquetado.

![Etiquetastolocas](/images/blog/201903_unidades/portada.png)

Para aquellos que vengan del CAD, el conocimiento de las funciones y parámetros para el diseño de impresiones de un SIG (composiciones en QGIS) es en principio una tarea ardua. Esto no significa que con un poco de dedicación y/o formación se lleguen a obtener  excelentes resultados. Siempre comparto con l@s alumn@s este enlace cuando trato este tema. Se merece, sin duda, dedicarle un buen rato.

Creo que un aspecto importante a tener en cuenta como base al empezar, es que **el SIG suele trabajar con los datos de forma dinámica**. Esto llevado a temas de diseño, supone que las dimensiones de grosores de líneas, patrones de rellenos, anchura de bordes, tamaño de tipografías, estilos, interlineado, espacio entre letras... se gestionan de forma automática y se adaptan a la escala de visualización en la que nos encontremos.

Eso no quita para que tengamos también la opción de usar unidades de medidas fijas que nos van a ser de utilidad cuando comencemos a diseñar nuestra composición en el "espacio papel". En este caso, las dimensiones definidas para simbología y etiquetado deberán ser pensadas para la escala de representación final  de la composición de mapa, y por lo tanto, ajustada a esta.

Aclaro que mi fuerte no es precisamente el diseño. Pero pensando concretamente en esto, creo que unos sencillos apuntes sobre este tema pueden ser de utilidad, sobre todo porque la documentación oficial en este sentido es escasa.

## Unidades en QGIS

Las unidades en QGIS, tanto para la altura de textos como para anchuras, desplazamientos o patrones, son las siguientes:

- Milímetros
- Puntos
- Píxeles
- Pulgadas
- Metros a escala
- Unidades de mapa

![Menú de unidades de QGIS](/images/blog/201903_unidades/menu_unidades.png)

*Menú de unidades de QGIS*

## Unidades para simbología/etiquetado dinámicos

Como he comentado, para que las dimensiones y medidas se adapten a la escala de la visualización, deben elegirse las unidades en milímetros, puntos, píxeles o pulgadas. Se suele usar por defecto los puntos o píxeles que son las unidades más frecuentes en diseño gráfico. En este aspecto también hemos de tener en cuenta la resolución de nuestra pantalla y el formato de exportación (p.ej.: a PDF) de una composición. Así, aunque definamos las equivalencia entre puntos y píxeles, el resultado será diferente si lo vemos en la vista de mapa que en la composición.

Consultando sobre este tema en el grupo de Telegram de usuarios de QGIS, [Agustín Gutiérrez](https://www.linkedin.com/in/agustingutierrezfornes/), cartógrafo y especialista en GIS, compartió este [enlace con un listado de equivalencias y porcentajes](https://reeddesign.co.uk/test/points-pixels.html).

Para generar las siguientes capturas, se han definido las unidades y los tamaños de textos y líneas para que en la vista de mapa se apreciaran todos iguales. Las capturas, sin embargo, están tomadas del Compositor. 

En la siguiente imagen se puede apreciar un ejemplo de equivalencia entre milímetros, puntos y píxeles.

![Ejemplo de Unidades para simbología/etiquetado dinámicos](/images/blog/201903_unidades/puntos_150.png)

*Ejemplo de Unidades para simbología/etiquetado dinámicos*


Si modificamos la escala de 1:150 000 a 1:50 000 podemos ver que la simbología no cambia:

![Ejemplo de Unidades para simbología/etiquetado dinámicos](/images/blog/201903_unidades/puntos_50.png)

*Cambio de escala y comportamiento*


##  Unidades para simbología/etiquetado estáticos

En estos casos debemos usar las unidades Metros a escala o Unidades de mapa. Estas pueden coincidir si trabajamos con sistemas de coordenadas proyectadas.  En mi caso uso unidades de mapa que además no dan problemas la renderizar la leyenda el el árbol de capas.

Estas unidades serán de gran ayuda cuando queramos dejar fijo el tamaño de etiquetas y grosores. Son también de utilidad cuando se personalizan las propiedades de etiquetas usando atributos. Cuando hacemos esto el sistema pasa de una visualización dinámica del etiquetado  aplicando un conjunto de reglas total, al diseño y personalización individual de cada. 

Siguiendo el ejemplo anterior y añadiendo el ejemplo de unidades de Puntos:

![Ejemplo de Unidades para simbología/etiquetado dinámico](/images/blog/201903_unidades/unidades_150.png)

*Ejemplo de Unidades para simbología/etiquetado estáticos*

Y para terminar la misma captura pero a diferente escala:

![Ejemplo de Unidades para simbología/etiquetado dinámico](/images/blog/201903_unidades/unidades_50.png)

*Cambio de escala y comportamiento*

**Formación:** Si estás interesado en formarte en este tema puedes consultar la información del próximo [**curso online “Sistemas de Información Geográfica QGIS y Urbanismo”**.](http://www.sigdeletras.com/2019/curso_on_line_sistemas_de_informacion_geografica_qgis_y_urbanismo_3_edicion/)
{: .notice--info}




