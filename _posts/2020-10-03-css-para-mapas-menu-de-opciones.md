---
title:  "CSS para mapas. Menú de opciones"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202009_css/02_header_css_color.gif" 
categories: 
  - 2020
tags:
  - css
  - javascript
  - webmapping
---


Vamos a continuar montando un visor de mapas sencillo que nos está sirviendo para dar un repaso a CSS.

En la entrada anterior, escribimos el código básico para tener una [mapa a pantalla completa](http://www.sigdeletras.com/2020/css-para-mapas-visor-a-pantalla-completa/) y que se adaptara a distintas resoluciones.

Ahora vamos a ver **cómo incluir una barra de menú superior con algunos botones que permitan realizar eventos de mapa usando OpenLayer**, una de las librería de mapas JavaScript más usadas.

## Cabecera con menú de opciones.

Partiremos del código de la entrada anterior que se encuentra en el [repositorio Github](https://github.com/sigdeletras/css-map).

La barra de navegación va a tener los siguientes elementos:
- Un título con el nombre de la aplicación (CSS Map, así todo loco)
- Botón para reiniciar el mapa a la vista inicial (Init view).
- Botón para ver el nivel de zum de la vista (Zoom level)
- Botón para obtener la extensión en WGS84 (EPSG:4326) del mapa. La función realiza una reproyección.

El código HTML usando [etiquetas semánticas de HTML5](https://developer.mozilla.org/es/docs/Sections_and_Outlines_of_an_HTML5_document) es el siguiente:

```html
<!-- index.html -->
...
    <header>
          <nav>
              <a class="logo" href="#">CSS MAP</a>
              <a id="init-view" href="#">Init View</a>
              <a id="view-zoom" href="#">Zoom level</a>
              <a id="view-extent" href="#">View Extent</a>
          <nav>
    </header>
...

```

Y aquí las líneas JavaScript.

```javascript
///map.js
...

function zoomTo(coordinates, zoom) {
  map.getView().setCenter(coordinates)
  map.getView().setZoom(zoom);
}

let initViewButton = document.getElementById('zoom-extend');
initViewButton.addEventListener('click', () => zoomTo(centerCoordinates, initialZoom));

function getZoomLevel() {
  let currentZoom = Math.round(map.getView().getZoom());
  alert(`Current Zoom Level: ${currentZoom}`)
}

let viewZoomButton = document.getElementById('view-zoom');
viewZoomButton.addEventListener('click', getZoomLevel);

function getCurrentExtent() {
  let currentExtent = map.getView().calculateExtent(map.getSize());
  let projectionCode = map.getView().getProjection().code_;
  let transformExtent = ol.proj.transformExtent(currentExtent, projectionCode, 'EPSG:4326');
  alert(`Extend: ${transformExtent.toString()}`)
}

let viewExtentButton = document.getElementById('view-extent');
viewExtentButton.addEventListener('click', getCurrentExtent);

...
```

Añadimos también una tipografía (Montserrat) a nuestra web, siguiendo los pasos que nos da [Google Fonts](https://fonts.google.com/specimen/Montserrat)

```css
/* style.css */
...

body {
    font-family: 'Montserrat', sans-serif;
}

```

Abrimos el navegador y vemos el (feo) resultado.

![Header sin CSS](/images/blog/202009_css/01_header_sin_css.png)

## Mejorando el diseño de nuestra barra de navegación.

Vamos a dar un poco de gracia a la barra de menú. Usando los selectores CSS de tipo y clase modificamos el **estilo de los elementos HTML tipo enlace**  que se encuentra dentro de *nav*.

Existen ciento y un páginas que nos ayudarán a elegir una **gama de color** en condiciones. Para la aplicación hemos usado la siguiente https://coolors.co/161925-23395b-406e8e-8ea8c3-cbf7ed

![Colors](/images/blog/202009_css/02_colors.png)

Un detallito que mejora la visualización es añadir **sombras a las cajas**. La mayoría de los frameworks css lo incorporan. No nos complicamos la vida. Obtenemos el código de sombreado para a barra de navegación desde otra [página web](https://www.cssmatic.com/box-shadow).

Al final el CSS ha quedado así.

```css
/* style.css */
...

      nav {
          overflow: hidden;
          background-color: #161925;
          -webkit-box-shadow: 0px 2px 5px 0px rgba(100, 100, 100, 1);
          -moz-box-shadow: 0px 2px 5px 0px rgba(100, 100, 100, 1);
          box-shadow: 0px 2px 5px 0px rgba(100, 100, 100, 1);
      }

      nav a {
          float: left;
          color: #f2f2f2;
          text-align: center;
          padding: 14px 16px;
          text-decoration: none;
          font-size: 17px;
      }

      nav a:hover {
          background-color: #8EA8C3;
          color: black;
      }

      nav a.logo {
          background-color: #23395b;
          color: white;
      }
...
        
```

Como remate final, al añadir la barra de opciones, la visualización de pantalla completa del mapa no funciona correctamente y nos aparece una barra de desplazamiento vertical. Tenemos más espacio de la vista al sumar los píxeles de la cabecera. 

Seguro que existen más opciones, pero he encontrado que podemos incluir una función dentro del CSS para realizar cálculos. La función es [calc()](https://developer.mozilla.org/es/docs/Web/CSS/calc) y la usamos para restar al tamaño de la vista el espacio del menú. 

Obtenemos el tamaño de la barra con las herramientas para desarrolladores del navegador.

![Alto header](/images/blog/202009_css/alto_menu.png)

Para terminar añadimos la función *calc* para obtener la altura de la caja del mapa.

```css
/* style.css */
...

.map {
    height: calc(100vh - 48px);
    width: 100%;
  }
...
```

## Conclusiones


Pongo la mano en el fuego de que el CSS que acabo de usar es muy mejorable. Es más, tras compartir la primera entrada, he recibido buenas referencias de amigos y conocidos para mejora el código. Al menos por eso, ya ha merecido la pena hacer esta serie de entradas.

Queda pendiente hacer la versión *responsive* de nuestro visor de mapas y añadir un panel lateral. 

Pero como digo, eso ya para el próximo fin de semana.

- [Web Ejemplo 2](http://www.sigdeletras.com/css-map/02_header_menu/index.html)
- Carpeta de código [02_header_menu](02_header_menu) en GitHub

![Header con CSS](/images/blog/202009_css/02_header_css_color.gif)


## Entradas relacionadas

- [CSS para mapas. Visor a pantalla completa](http://www.sigdeletras.com/2020/css-para-mapas-visor-a-pantalla-completa/)




