---
title:  "Mapeando el comercio de cercanía frente al COVID19"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/images/blog/202003_covid19/portada.png" 
categories: 
  - 2020
tags:
  - openstreetmap
  - coronavirus
---

Hoy domingo 15 de marzo he participado en una **reunión informativa de "Geo-voluntarios COVID19"** organizado por el grupo de [Geo Developer](https://www.meetup.com/es-ES/Geo-Developers/) que lleva Raúl Jimenez [@hhkaos](https://twitter.com/hhkaos). Os dejo la [grabación de esta primera reunión](https://www.youtube.com/watch?v=5v5nKNqiaXM).

El grupo ha surgido de forma natural frente a la complicada situación que estamos viviendo debido a la pandemia provocada por el Covir-19. La **finalidad de poder crear un grupo de volutarios que pueda desempeñar distintas labores de apoyo basadas en la aplicación de las tecnologías geográficas** (mapeado infraestructuras y servicios, diseño de mapas informativos, desarrollo de aplicaciones basadas en la geolocación).


Dándole vueltas durante la hora de la comida, he pensado que una **labor de utilidad** que cualquiera que se maneje con un ordenador y sepa conectarse a Internet podría ser la es **la incorporación en [OpenStreetMap](https://wiki.openstreetmap.org/wiki/Main_Page) de datos vinculados con el comercio de cercanía (panaderías, pescaderías, carnicerías...)**. La compra de productos alimenticios en este tipo de negocios minoristas puede ayudar a mantener la economía a este nivel de "barrio" y además favorecerá la descongestión en las grandes superficies que tantas imágenes alarmantes nos está dando.

Muchos pensarán que para esto ya está Google Maps. Pues es verdad, pero la cuestión es que la mayoría de estos pequeños comercios no están en Google Maps. Quizás esto se deba a que los dueños de este tipo de establecimientos no tengan habilidades técnicas para dar su negocio de alta. Por otra parte, **los datos de OpenStreetMap son abiertos y pueden ser reutilizados** por ejemplo, para hacer mapas específicos con la localización de estos locales. Esto favorecerá la reducción de los recorridos para la compra del día a día siguiendo así las recomendaciones gubernamentales.

En primer lugar he buscado los datos de alguno de los tipo de estos comercios en mi ciudad, Córdoba y el resultado es sin duda desolador (ej. ¡¡¡¡10 panaderías!!!!!)

![Panaderías Córdoba](/images/blog/202003_covid19/panaderias.png)

[Visor de panaderías en Córdoba](https://overpass-turbo.eu/map.html?Q=%2F*%0AThis%20has%20been%20generated%20by%20the%20overpass-turbo%20wizard.%0AThe%20original%20search%20was%3A%0A%E2%80%9Cshop%3Dbakery%E2%80%9D%0A*%2F%0A%5Bout%3Ajson%5D%5Btimeout%3A25%5D%3B%0A%2F%2F%20gather%20results%0A(%0A%20%20%2F%2F%20query%20part%20for%3A%20%E2%80%9Cshop%3Dbakery%E2%80%9D%0A%20%20node%5B%22shop%22%3D%22bakery%22%5D(37.86286053226588%2C-4.8319244384765625%2C37.913799781025396%2C-4.722833633422852)%3B%0A%20%20way%5B%22shop%22%3D%22bakery%22%5D(37.86286053226588%2C-4.8319244384765625%2C37.913799781025396%2C-4.722833633422852)%3B%0A%20%20relation%5B%22shop%22%3D%22bakery%22%5D(37.86286053226588%2C-4.8319244384765625%2C37.913799781025396%2C-4.722833633422852)%3B%0A)%3B%0A%2F%2F%20print%20results%0Aout%20body%3B%0A%3E%3B%0Aout%20skel%20qt%3B)


Añadir estos datos en OpenStreetMap es muy sencillo.

1. Accedemos a OpenStreetMap en esta dirección https://www.openstreetmap.org
2. Nos registramos si somos usuarios nuevos o metemos nuestros datos si ya somos usuarios.
3. Localizamos la zona qu vayamos a mapear, por ejemplo nuestra calle, el barrio...
4. Hacemos clic en Editar. el mapa de fondo cambiará, viéndose un mapa aéreo y los objetos que ya existen.
5. Una vez localizado el lugar donde queramos añadir algún comercio, hacemos click en la herramienta Punto.
6. situado el comercio añadimos como mínimo el tipo de tienda, usando el formulario de la derecha. Solo tenemos que introducir el tipo, por ejemplo panadería, carnicería, frutería
7. Podemos seguir añadiendo de esta forma más puntos o bien guardar los datos
8. Antes de terminar añadimos un breve comentario E. "Comercio de cercanía del Zoco" y listo.

![Panaderías Córdoba](/images/blog/202003_covid19/crear_panadería.gif)

Estos datos posteriormente podrán ser usados dentro de aplicaciones móviles o para calcular rutas a pie a las tiendas más cercanas.

Como se puede comprobar es un **acto sencillo, que podemos hacer desde casa, incluso con los niños o los jóvenes, y que pueden ayudar en diferentes aspectos a combatir el maldito Coronavirus**.

!!!Mucho ánimo!!!! [#YoMeQuedoEnCasa](https://twitter.com/search?q=%23YoMeQuedoEnCasa&src=typeahead_click)
