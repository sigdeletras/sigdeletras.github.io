---
title:  "CSS para mapas. Visor a pantalla completa"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202009_css/03_vh.gif" 
categories: 
  - 2020
tags:
  - css
  - javascript
  - webmapping
---


**HTML, CSS y JavaScript** son los tres lenguajes básicos para poder desarrollar una aplicación web.

De estas tres patas del banco, CSS es sin duda mi talón de Aquiles. Me preocupo en leer documentación, usar lo más correctamente las opciones del lenguaje, organizar los archivos de estilo...pero nada, no tengo la sensación de control que puedo tener picando JavaScript.

Mi respuesta "digna" a esto es usar un **framework CSS**. Muchos de los visores de mapas web que he realizado están basados en  [Bootstrap](https:/getbootstrap.com/) y me gusta bastante [W3.CSS](https:/www.w3schools.com/w3css/defaulT.asp) que lo usé durante mis estudios de desarrollo web.

Ahora estoy con [Material UI](https:/material-ui.com/) para proyectos con la librería React. Pero hay frameworks para aburrirse: [Bulma](https:/bulma.io/), [Ant](https:/ant.design/), [Tailwind](https:/tailwindcss.com/)...

![Ejemplo OSM](/images/blog/202009_css/01_material_UI.png)


Usar este tipo de herramientas está bien (me lo digo yo y miles de desarrolladores). A pesar de esta autoafirmación, creo que **para diseños rápidos, si estamos comenzando en esto del desarrollo o queremos tener control total del diseño es mejor usar directamente CSS**. 

He pensado realizar serie de entrada donde describir, **cómo hacer un diseño sencillo de una aplicación web de mapas con CSS**. Serán entradas muy básicas, a todas luces mejorable, pero creo que puede ser útil para mucha gente y para mi mismo.

El código se encuentra en [GitHub](https:/github.com/sigdeletras/css-map).  Espero poder ir añadiendo los recursos que surjan de estas entradas.

## Diseño de partida.

Echando un vistazo a páginas web de mapas como [Google Map](https:/www.google.es/maps/preview), [OpenStreetMap](https:/www.openstreetmap.org/search?query=roma#map=10/41.8992/12.5450&layers=C) o [Here](https:/wego.here.com/?x=ep&map=40.4172,-3.684,10,normal), podemos decir que de forma general las aplicaciones cuentan con:
- Barra superior con opciones de menú.
- Panel lateral con herramientas (ej. leyenda, control de capas, gestión de capas..) y paneles informativos (resultados de búsqueda, detalles).
- Área destinada al mapa.

![Ejemplo OSM](/images/blog/202009_css/01_osm.png)

Sin duda esta división es la básica. Existen muchos otros visores de mapas con diseños muy trabajados. Pero para el objetivo de esta entrada nos vamos a quedar con esta simplificación. 

Realizar un boceto de lo que va a ser nuestra página web es muy importante. Además de dejar clara la estructura de la aplicación respecto a los elementos HTML que debe incluir, es de utilidad por ejemplo para hacer un primer listado de componentes si trabajamos con React.

Como debemos empezar por algún sitio y como lo que verdaderamente nos gusta son los mapas ¿porqué no comenzar por aquí?

## CSS para un mapa a pantalla completa.

Vamos a usar como punto de partida el ejemplo de [Quick-start de OpenLayers](https:/openlayers.org/en/latest/doc/quickstart.html) pero separando el CSS y el código JavaScript en diferentes archivos.

La aplicación cuenta con los siguientes ficheros:
- index.html
- style.css
- map.js

![Basic map](/images/blog/202009_css/01_index.png)


En nuestro archivo *map.css* tenemos el siguiente código que se usará para dibujar nuestra caja de mapa con el id 'map' y la clase CSS del mismo nombre

```css
.map {
    height: 400px;
    width: 100%;
  }
```

![Basic map](/images/blog/202009_css/02_basic_map.png)

Lo más común es querer que nuestro mapa ocupe la extensión completa del navegador y que además se ajuste al tamaño del mismo si lo ajustamos.

Cuando estamos empezando en esto del desarrollo web, y aplicando una lógica aplastante, tendemos a pensar que si el ancho de la página se soluciona dando un tamaño del 100%, podemos hacer los mismo con el alto. Pero desgraciadamente esto no es tan sencillo. Si probamos podemos ver que el mapa desaparece.

El porcentaje sobre un *height* se aplica sobre el número de píxeles del elemento padre que en nuestro caso sería el body, y ya que este no está definido el mapa no se representa. 

El siguiente razonamiento es obtener el ancho de nuestra pantalla actual y usarlo para la anchura del mapa. Pero,  ¿qué ocurre cuando usamos otra resolución?. Para resoluciones más pequeñas tendremos que usar las barras de desplazamiento y para las superiores a la definida estaremos de nuevo el punto de partida.

Lo más sencillo es indicar que la **anchura se ajuste al tamaño de la ventana de visualización (viewport)  esto se usa con la [unidad de medida vh (Viewport Height)](https://www.sitepoint.com/css-viewport-units-quick-start/)**. Con esta unidad, el valor indicado representa el porcentage de pantalla a ocupar. Así, 100vh significa el 100% de la ventana de visualización.

```css
.map {
    height: 100vh;
    width: 100%;
  }
```

Para que esta regla funcione correctamente debemos borrar el margen que trae por defecto el navegador. Modificamos el archivo CSS eliminando los márgenes para el elemento HTML y el body.


![Basic map](/images/blog/202009_css/02_margenes.png)

Cambiamos el CSS para que queda como vemos en el código que sigue. 


```css
html, body {
     margin: 0; 
     padding: 0; 
}

.map {
    height: 100vh;
    width: 100%;
  }
```

*Tras publicar la entrada en Linkedin, mi compañero y diseñador y maquetador web [Luis Guzmán](https://www.linkedin.com/in/luis-guzm%C3%A1n-rubio-a426435b/) me recomendó usar un [reset](https://es.wikipedia.org/wiki/Reset_CSS) con el que establecer unos valores iniciales para el formato de elementos HTML. Entre las opciones se encuentra [Normalice.css](https://necolas.github.io/normalize.css/)*

Conseguiremos tener nuestro mapa a pantalla completa y que se reajusta con el tamaño del visor.

![Basic map](/images/blog/202009_css/03_vh.gif)

Esta es la primera entrada sencilla sobre este tema y espero que sea de utilidad. En las siguientes, irenos avanzando en este tema añadiendo por ejemplo una barra superior a modo de menú y el panel lateral.

- [Web Ejemplo 1](http://www.sigdeletras.com/css-map/01_full_viewport/index.html)
- Carpeta de código [01_full_viewport](https://github.com/sigdeletras/css-map/tree/master/01_full_viewport) en Github

## Entradas relacionadas

- [CSS para mapas. Menú de opciones](http://www.sigdeletras.com/2020/css-para-mapas-menu-de-opciones/)
- [CSS para mapas. Flexbox y diseño responsive](http://www.sigdeletras.com/2020/css-para-mapas-flexbox-y-diseño-responsive/)



