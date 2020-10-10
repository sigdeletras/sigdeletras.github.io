---
title:  "CSS para mapas. Flexbox y diseño responsive"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202009_css/03_responsive.gif" 
categories: 
  - 2020
tags:
  - css
  - javascript
  - webmapping
  - responsive
  - flexbox
---
Seguimos con las entradas sobre uso de CSS para diseño de visores de mapas. En los textos anteriores, montamos sencilla [aplicación *webmapping* para que se viera a pantalla completa](http://www.sigdeletras.com/2020/css-para-mapas-visor-a-pantalla-completa/). Posteriormente añadimos una [barra superior de opciones](http://www.sigdeletras.com/2020/css-para-mapas-menu-de-opciones/). En esta ocasión, vamos a modificar nuestro código CSS para que la barra de opciones sea adapte a distintos dispositivos, lo que se conoce como diseño *responsive*

## Variables en CSS

Gracias a las aportaciones en Linkedin de mi compañero [Luis Guzmán ](https://www.linkedin.com/in/luis-guzm%C3%A1n-rubio-a426435b/) hemos incorporado el uso de [variables CSS](https://developer.mozilla.org/es/docs/Web/CSS/Using_CSS_custom_properties). Dejo un enlace bastante reciente sobre [variables CSS](https://ishadeed.com/article/css-vars-101/) que me resulta muy completo.

Podemos definir, por ejemplo los colores de nuestra aplicación o las tipografías que vamos a usar en la página y luego llamarlas dentro del código CSS usando la [función var()](https://developer.mozilla.org/es/docs/Web/CSS/var).

```css
/* style.css */

/* Varibles */
:root {
    /* Colors */
    --bg-header: #161925;
    --bg-header-hover: #8EA8C3;
    --font-color-nav: #f2f2f2;
    --bg-logo: #23395b;
    /* Fonts */
    --font-family-body: 'Montserrat', sans-serif;
}

/* Basic rules */

body {
    font-family: var(--font-family-body);
}


```

## Usando Flexbox

Flexbox, es un modelo de diseño CSS3 que permite que los elementos HTML que se encuentran dentro de un contenedor, se organicen automáticamente dependiendo del tamaño de la pantalla o del dispositivo.

El ajuste de tamaños y disposición pueden hacerse en CSS sin usar Flexbox con display, float.... pero es sin duda más complejo.

Para saber más sobre este tipo de diseño os recomiendo la visita a la página [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) con gran cantidad de esquemas visuales sobre los parámetros de Flexbox.


Para nuestro visor de mapas hemos realizado los siguientes cambios.

```css
/* style.css */

nav {

    display: flex;
    flex-direction: row; 
    flex-wrap: wrap;
    justify-content: flex-start;

    overflow: hidden;
    background-color: var(--bg-header);
    -webkit-box-shadow: 0px 2px 5px 0px rgba(100, 100, 100, 1);
    -moz-box-shadow: 0px 2px 5px 0px rgba(100, 100, 100, 1);
    box-shadow: 0px 2px 5px 0px rgba(100, 100, 100, 1);

}
```
El selector nav, que será nuestro contenedor, tiene las siguientes propiedades:

- [display: flex](https://developer.mozilla.org/es/docs/Web/CSS/display) Establecemos la propiedad display de la caja *nav* como *flex*. Esto indica que todos los elementos hijos dentro de este contenedor se ajustarán al diseño flexible por cajas.
- [flex-direction](https://developer.mozilla.org/es/docs/Web/CSS/flex-direction) La propiedad se usa para especificar el eje principal y la dirección de los objetos dentro del contenedor. Podemos disponerlos como filas (*row*) o columnas (*column*) y con dirección normal o al revés.
- [flex-wrap](https://developer.mozilla.org/es/docs/Web/CSS/flex-wrap) especifica si los elementos "hijos" son obligados a permanecer en una misma línea (*wrap*) o pueden fluir en varias líneas (*nowrap*).
- [justify-content](https://developer.mozilla.org/es/docs/Web/CSS/justify-content) distribuye el espacio entre y alrededor de los items flex, a lo largo del eje principal de su contenedor. Hemos usado *flex-start* para alinear las opciones del menú desde el comienzo.

![Flex properties](/images/blog/202009_css/03_flex_properties.gif)


Si usáis el editor de código Visual Studio Code se puede instalar el complemento **CSS Flexbox Cheatsheet** que ofrece ayuda contextual sobre Flexbox y una "chuleta" con todas las propiedades.

![CSS Flexbox Cheatsheet](/images/blog/202009_css/03_flexbox_chearsheet.png)

## Diseño *responsive*

Usando las reglas CSS podemos diseñar nuestra aplicación para que se adapta a móviles o tablets. El **diseño adaptativo o *responsive* está enfocado en  redimensionar y colocar los elementos de la web de forma que se adapten al ancho de cada dispositivo permitiendo una correcta visualización y una mejor experiencia de usuario**.

Para aplicar un estilo a una determinada resolución se usa la [regla-at CSS @media](https://developer.mozilla.org/es/docs/Web/CSS/@media) asocia un grupo de declaraciones anidadas.

![](/images/blog/202009_css/03_screen.png)

*Autor: Muhammad Rafizeldi (MRafizeldi) / CC BY-SA (https://creativecommons.org/licenses/by-sa/3.0)*

Las dimensiones generales de los distintos dispositivos son las que se encuentran en la imagen superior. Para simplificar el ejemplo hemos definido las reglas para dispositivos de ancho máximo de 768px (tablets) y de 480px (móviles).

Para tabletas, el logo ocupará una primera línea a ancho total y los botones se ajustarán al espacio en una segunda línea
```css
/* style.css */

@media all and (max-width: 768px) {
    nav {
        justify-content: space-around;
    }
    nav a.logo {
        flex: 100%;
    }
    .map {
        height: calc(100vh - 96px);
    }
}
```

Si vemos la aplicación en dispositivos móviles, los elementos se dispondrán en filas, alineados al centro y con bordes para diferenciarlos.

```css
/* style.css */

@media all and (max-width: 480px) {
    nav {
        flex-flow: column wrap;
        padding: 0;
    }
    nav a {
        padding: 10px;
        border-top: 1px solid rgba(255, 255, 255, 0.3);
    }
    .map {
        height: calc(100vh - 168px);
    }
```

Vemos un animación del resultado a distintas resoluciones.

![Responsive version](/images/blog/202009_css/03_responsive.gif)

## Mejorando nuestro visor con algo de JavaScript

No mi intención en estas entradas hablar el desarrollo de JavaScript aplicado al desarrollo de aplicaciones de mapas. De todas formas, no puedo resistirme a añadir algunas pequeñas mejoras al visor.

En esta rama versión del visor añadido código para la **incorporación de dos mapas base** más: uno el servicio WMS del PNOA con datos del mapa base del IGN y el segundo, uno de los estilo de renderizado sobre OpenStreetMap de la web de [Stamen](http://maps.stamen.com/#terrain/12/37.7706/-122.3782).

Para gestionar la visualización de las nuevas capas base he usado el módulo [OpenLayers LayerSwitcher](https://github.com/walkermatt/ol-layerswitcher) que añade un **control de capas visual**.

![LayerSwitcher with Stamen](/images/blog/202009_css/03_stamen.png)

## Recursos en GitHub

- [Web Ejemplo 3](http://www.sigdeletras.com/css-map/03_flexbox_responsive/index.html)
- Carpeta de código [03_flexbox_responsive](https://github.com/sigdeletras/css-map/tree/master/03_flexbox_responsive) en GitHub


## Entradas relacionadas

- [CSS para mapas. Visor a pantalla completa](http://www.sigdeletras.com/2020/css-para-mapas-visor-a-pantalla-completa/)
- [CSS para mapas. Menú de opciones](http://www.sigdeletras.com/2020/css-para-mapas-menu-de-opciones/)




