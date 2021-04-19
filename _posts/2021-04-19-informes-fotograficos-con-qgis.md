---
title:  "Informes fotográficos con QGIS"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202104_informes/" 
categories: 
  - 2021
tags:
  - qgis
  - informes
---

# Informes fotográficos con QGIS usando HTML

En el mundo de la informática, creo que rara vez se no se puede encontrar una solución a un determinado "problema". Cuando algún compañero, cliente, alumno o amigo me pregunta sí se puede realizar un proceso concreto con SIG o desarrollar una función dentro de una aplicación web, mi respuesta es siempre SÍ, sí se puede. 

Esta respuesta categórica, está sin embargo vinculada con una serie de cuestiones que debemos tener en consideración. Partiendo de los conocimientos y experiencia que nosotros o nuestro equipo tenga ¿seremos capaces de hacerlo?, ¿cuánto tiempo (coste) tardaremos en hacerlo?, ¿nos será rentable, en sentido no estrictamente económico del término, hacerlo? ¿nuestras herramientas son lo suficientemente versátiles y potentes para ofrecer una solución?, ¿la respuesta que planteemos será la óptima? o simplemente ¿nos apetece remangarnos y dedicarle parte de nuestro tiempo a encontrar un desenlace a todo esto?

## Historia de usuario y análisis de requisitos

Tras muchos años usando QGIS a nivel profesional, rara vez me han planteado algo que no tenga solución con este SIG de código abierto. Como he comentado en la introducción, es todo cuestión de tiempo, experiencia y ganas de ponerse. 

QGIS cuenta con las funcionalidades  suficientes para dar respuesta a la mayoría de las cuestiones de índole geográfico que necesiten un análisis espacial o representación cartográfica. Por si fuera poco, gracias a expresiones y las posibilidades que nos da el uso de Python en su API, podemos decir que las limitaciones vienen dadas más por nuestros conocimientos que por la aplicación.

La semana pasada una compañera del grupo de Geoinquietos Córdoba, me planteaba una duda **¿se puede sacar un informe de mapas de situación de unas localizaciones y añadir un reportaje de fotografías relacionadas?** Mi respuesta fue "seguro que sí, pero yo ahora mismo no sabría decirte cómo".

Aprovechando el fin de semana, y tras darle alguna que otra vuelta, creo que he dado una solución.

Si este trabajo nos lo hubiera solicitado un cliente, y aplicando metodologías ágiles lo primero que deberíamos hacer es analizar la historia de usuario.

Partiendo de la pregunta que me hicieron, este podría ser un ejemplo de historia de usuario.

*Como usuario quiero generar un informe con QGIS para representar mapas con la situación y los datos de la toma de datos en campo, acompañado de las fotografías realizadas*.

Ahora vamos a obtener los requisitos
- El informe estará hecho desde QGIS.
- Debemos de contar con dos datos de entrada: una capa de localización de toma de datos y una tabla con el listado de las las fotografías tomadas en cada visita.
- Nuestra salida será una composición con los mapas de localización.
- Para cada mapa de situación se adjuntará una galería de imágenes vinculadas (relación) con la localización.

Utilizaré como datos de prueba las fotografías del  [Banco Audiovisual de la 
Red de Información Ambiental de Andalucía (REDIAM)](http://www.bancoaudiovisual.juntadeandalucia.es/medioambiente/start/index). De manera genérica los materiales de esta recopilación están bajo las condiciones que ofrece la Licencia Creative Commons (by-nc-nd 4.0 España). 


## Mapas de localización

Si conocemos nuestro SIG, sabemos que gracias a la herramienta Atlas de QGIS podemos diseñar plantillas de composiciones que representarán datos de una capa de cobertura o índice. 

El diseño del mapa plantilla incluye el mapa de ubicación sobre la ortofotografía del PNOA, los elementos cartográficos básicos (escala, norte, cuadrícula y mapa de referencia) y los datos sobre la capa de ubicaciones (id, descripción, fecha y coordenadas calculadas del punto)

![Atlas de QGIS](/images/blog/202104_informes/01_atlas.png)

## Galería de imágenes

Usando un elemento de tipo Imagen en las composiciones solo podemos definir la ruta de una imagen específica. Esto nos servirá si tuviéramos una única foto por inspección. 

Pero como podemos apreciar, el desarrollo necesita representar varias fotografías de una única localización o lo que se traduce a nivel de datos en una relación 1:N.

El proyecto contiene una tabla con el listado de fotografías asociadas a la visita. Las tablas están relacionadas mediante el código de la inspección.

![Subformulario QGIS con fotografía](/images/blog/202104_informes/02_subformulario.png)


Llegado a este punto, el problema a resolver  es ¿cómo añadir la galería de fotos asociadas a la inspección en la composición de Atlas?

Mi primer acercamiento fue añadir los datos como  tabla filtrando los resultados por el campo de relación entre ambas. Para que solo se muestren las filas relacionadas definimos un filtro.

```
"codruta" = attributes( @atlas_feature )['cod']
```

![Filtrado de tabla dentro de mapa de QGIS](/images/blog/202104_informes/03_tabla_filtrada.png)

Con esta solución resolvemos el tema del filtro pero no podemos representar las imágenes. 

# Usando la función aggregate

QGIS permite obtener un valor calculado a partir de relaciones entre tablas usando la función aggregate. Dentro de las opciones de la función se encuentra *concatenate* que nos va a devolver una cadena con la concatenación de valores de un campo (expresión) concreto.

Si añadimos la función dentro de una expresión podríamos obtener la cadena con el listado de fotos.

La expresión sería la siguiente:

```
aggregate(layer:='listado_fotos',aggregate:='concatenate', expression:= "img", 
filter:= "codruta" =attributes( @atlas_feature )['cod'], 
concatenator:=' - ')
```

Vemos el texto que nos devuelve la expresión.

![Ejemplo de función aggregate en QGIS](/images/blog/202104_informes/04_aggregate.png)

## HTML dentro de expresiones

Vamos a avanzar un poco más. QGIS permite representar como código HTML la información de un campo de tipo texto.

Si modificamos la expresión para que el resultado sea el código HTML que incluye un elemento de tipo imagen, ya podríamos solucionar el requisito principal de nuestro proyecto.

```
aggregate(layer:='listado_fotos',aggregate:='
concatenate', 
expression:= 
'<p><img src="file:///C://fotos/' || "img" || 
'" width="500px" height=""></p>', 
filter:= "codruta" =attributes( @atlas_feature )['cod'])
%]

```

![Ejemplo de función aggregate en QGIS con código HTML](/images/blog/202104_informes/05_aggregate_html.png)

## Mejorando el informe con elementos HTML

Parece que con la solución anterior hemos dado respuesta a las necesidades de nuestro usuario. Pero esto no es del todo correcto. Como todo desarrollo debemos realizar una serie de test que pongan a prueba nuestra propuesta. 

Lo primero que podemos probar es qué ocurre si la galería de fotos es numerosa o si aumentamos su tamaño. Añadiendo algunas imágenes más podemos ver que se saldrían de la página. Podremos disminuir el tamaño de la imagen, pero no sería la mejor solución.

![Galería de imágenes dentro de composición de QGIS](/images/blog/202104_informes/06_muchas_imagenes.png)

Si volvemos a la herramienta, podemos encontrar que **QGIS permite añadir en sus composiciones de mapas elementos HTML**. Gracias a sus opciones, QGIS gestionará de forma inteligente el salto entre páginas.

Tras insertar el marco HTML, completamos la información con un HTML básico en el que hemos añadido la expresión con la función aggregate dentro del body.

```html
<!DOCTYPE html>
<html lang="en">
<body>
  [%
  aggregate(layer:='listado_fotos',aggregate:='
  concatenate', 
  expression:= 
  '<div>'||
  '<p><img src="file:///'||  @project_folder || '/' || "img" || '" width="90%" height="100%"></p> '||
  '<p>'|| "codfoto"||' '|| "titulo"||' '|| '</p> '||
  '</div>', 
  filter:= "codruta" =attributes( @atlas_feature )['cod'])
  %]
 </body>
</html>

```
Podríamos mejorar el resultado sacando el máximo provecho a los sistemas de distribución de elementos HTML basados en CSS como Flexbox o CSS Grid pero eso en principio con esto ya estamos obteniendo la solución a nuestro desarrollo.


    <iframe width="560" height="315"
src="https://youtu.be/U_Cpi75ZUqo" 
frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen></iframe>

