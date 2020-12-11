---
title:  "BuscaCalles. Aplicación React para la consulta de datos de CartoCiudad"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202012_buscacalles/principal.png" 
categories: 
  - 2020
tags:
  - desarrollo web
  - react
  - cartociudad
---
Aprovechando los días de fiesta del largo puente de la Constitución, he ido sacando ratos para poder terminar una aplicación web que tenía iniciada hace algún tiempo. 

A modo de *side project*, la finalidad principal ha sido la de seguir profundizando en el desarrollo de web tipo aplicación de página única (SAP) usando la librería JavaScript React.

El objetivo principal del proyecto era realizar una **web de búsquedas de calles, topónimos y poblaciones de España usando el servicio API REST del proyecto CartoCiudad**.

La primera versión de la web que he denominado **BuscaCalles** se encuentra accesible en la dirección web [http://sigdeletras.com/buscacalles-cartociudad/](http://sigdeletras.com/buscacalles-cartociudad/).

![BuscaCalles. Página principal](/images/blog/202012_buscacalles/principal.png)

Desde el punto de vista técnico, el proyecto ha estado centrado en las siguientes habilidades:

- **Crear componentes funcionales de React**. Cuando comencé a aprender React usé componentes basados en clases.
- **Usar los Hooks** básicos de React como *useState*, para manejar el estado de los componentes o *useEffects* para la gestión del ciclo de vida del componente.
- **Diseñar la aplicación con CSS puro**, sin usar ningún framework CSS como Bootstrap. Quería seguir practicando con variables CSS, *media queries*, diseño *responsive*.

## API REST de CartoCiudad

El punto de partida fue el conocimiento del servicio API REST de CartoCiudad. CartoCiudad es *“una base de datos con cobertura nacional que contiene la siguiente información: red viaria continua, cartografía urbana y toponimia, códigos postales y divisiones censales”*.

El proyecto está coordinado por el Instituto Geográfico Nacional (IGN) y se genera a partir de datos oficiales del IGN, la Dirección General del Catastro (DGC), el Instituto Nacional de Estadística (INE) y el Grupo Correos. Además, colaboran en su elaboración y mantenimiento varias comunidades autónomas. 

Puede consultarse toda la información es su página web [http://www.cartociudad.es/portal/](http://www.cartociudad.es/portal/)

Dentro del proyecto se engloba datos para su descarga, servicios de mapas web de visualización, descarga y geoprocesamiento. La iniciativa incluye un servicio API REST que es el que he usado en la aplicación.

En la [documentación técnica](https://www.cartociudad.es/recursos/Documentacion_tecnica/CARTOCIUDAD_ServiciosWeb.pdf) de los servicios, podemos consultar en los distintos servicios REST de cálculos geográficos sobre la información de la base de datos.

En esta primera versión de la aplicación, se realiza una petición de tipo GET de geocodificación denominada ‘candidates’ que permite obtener los resultados más aproximados a la búsqueda introducida en formato JSONP.

[http://www.cartociudad.es/geocoder/api/geocoder/candidatesJsonp?q=plaza de las tendillas&limit=4](http://www.cartociudad.es/geocoder/api/geocoder/candidatesJsonp?q=plaza%20de%20las%20tendillas&limit=4)

![01_peticion_get_candidates](/images/blog/202012_buscacalles/01_peticion_get_candidates.png)

El análisis de los resultados obtenidos es fundamental para el diseño de los procesos de la aplicación. Así, además de la búsqueda, se ha implementado una opción de filtro que elimina los resultados de municipios, poblaciones o ambos, obteniendo solo los datos de tipo callejero.

## Diseño

Me ha sido muy útil dedicar un tiempo al diseño propio de la aplicación sin tener que pensar en la lógica. Para ello, ha sido de mucha ayuda hacer un boceto en HTML básico, sin usar React. 

De este primer diseño surgió en primer lugar el CSS y poco a poco cada uno de los componentes que luego programé en React.

Como he comentado, he preferido trabajar directamente con CSS sin ningún framework. Quizás sea uno de los puntos de los que más contento estoy, no tanto por el diseño final, que seguro es muy mejorable, sino por todo lo aplicado y aprendido.

He usado variables CSS para definir el tamaño de letra, la tipografía y los colores de la aplicación. Flexbox me ha dado juego para hacer el diseño responsivo de la web. Tras ver un vídeo de CodelyTV ()sobre[ 5 Grandes Errores con CSS Layouts](https://www.youtube.com/watch?v=C1J__Iz1CH4), he usado en todo lo posible em como unidad de medida. Y, para terminar, descubrí recientemente la metodología CSS BEM que he intentado seguir para los nombres de las reglas.

## Desarrollo con React

Tras este diseño inicial, identifiqué los siguientes componentes que han sido programados con funciones de React.

- *Header*. Barra de navegación superior con algunos enlaces: web SIGdeletras, enlace a esta entrada y acceso al repositorio GitHub
- *SearchTools*. Sección principal con el título de la web y los elementos para realizar las búsquedas: caja de texto, opciones de filtrado y botón de reset.
- *InfoBlocks*: Sección con bloques HTML básicos con información previa de la página.
- *Information*. Caja para la presentación de los resultados, tanto del listado de etiquetas por provincias como los resultados en tarjetas. Incluye los componentes InfoBlocks y Candidates
- *Candidates*. Componente con el conjunto de resultados en tarjetas.
- *Card*. Tarjeta básica con información del elemento: nombre, tipo, código postal, provincia y mensaje de grado de coincidencia.

![Componentes](/images/blog/202012_buscacalles/componentes.png)

Los componentes se encuentran en la carpeta */components* y están formados por su fichero JavaScript y el correspondiente CSS.

Como he comentado, he creado componentes basados en funciones y no en clases. Además de ser la forma recomendable de programar los componentes con React, y de haber documentación sobre esto en la misma página del proyecto y muchas webs, para mí ha sido mucho más sencillo poder usar funciones.

De forma general, los componentes funcionales ofrecen mayor claridad en el código y permiten usar [Hooks](https://es.reactjs.org/docs/hooks-intro.html) que simplifican bastante el uso del estado y manejo del ciclo de vida de los componentes React.

La estructura de un componente básico en nuestra aplicación es por ejemplo la tarjeta con datos (Card)

![Componentes funcional Card](/images/blog/202012_buscacalles/02_card.png)

## Hooks

Entre los [Hooks disponibles](https://es.reactjs.org/docs/hooks-reference.html ) para esta primera vez he usado principalmente *useState* y *useEffect*.

Gracias a [useState](https://es.reactjs.org/docs/hooks-reference.html#usestate), tenemos un valor con estado y una función para actualizar. Dentro de nuestra componente SearchTools existía una variable que almacenaba el listado de objetos con los datos de los candidatos tras realizar la consulta a la API de CartoCiudad. Con los datos, teníamos la función para su actualización que se ejecutaba por ejemplo al cambiar las opciones de filtrado.

![useState](/images/blog/202012_buscacalles/03_usesate.png)

El otro Hooks básico es [useEffect](https://es.reactjs.org/docs/hooks-reference.html#useeffect). Recomiendo este [artículo](https://midu.dev/react-hooks-use-effect-funcionalidad-en-el-ciclo-vida-componentes/) del desarrollador Miguel Ángel Durán [@midudev](https://twitter.com/midudev) donde se explica claramente para qué sirve este hook. En el artículo se indica que useEffect *recibe como parámetro una función que se ejecutará cada vez que nuestro componente se renderice, ya sea por un cambio de estado, por recibir props nuevas o, y esto es importante, porque es la primera vez que se monta*.

Dentro de la aplicación, usamos useEffect para llamar a la función que hace la petición REST a CartoCiudad según los criterios definidos. Una vez llamada, cambiaremos los datos de los candidatos que hemos definido con useState.

![useEffect](/images/blog/202012_buscacalles/04_useEffects.png)

## Función getCandidates

La función que realiza la petición de datos a la API y que es llamada usando *useEffect*, se ha generado en una carpeta dedicada a almacenar la consulta a servicios.

Es una función [asíncrona](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Sentencias/funcion_asincrona) que devuelve el JSON con los datos.

Como detalle, quiero comentar que la API de CartoCiudad no devuelve los datos directamente en JSON sino en una envoltura, o lo que es lo mismo en JSONP. En JSONP en lugar de enviar solo el dato, lo que se envía es una función, normalmente llamada *callback*, que es como un JavaScript que engloba el dato que hemos solicitado. Gracias a JSONP se solucionan situaciones de *cross-domain*.

Debido a esto, el proyecto incorpora la librería [fetch-jsonp](https://www.npmjs.com/package/fetch-jsonp).

![getCandidates](/images/blog/202012_buscacalles/05_fetchjsonp.png)

## Conclusiones y temas pendientes

La experiencia ha sido realmente positiva. Al menos para mí, realizar este tipo de proyectos paralelos, sin presiones y simplemente por el mero hecho de aprender tiene muchas ventajas. 

Cada vez me gusta más React y aprender el funcionamiento básico de los Hooks mejora sin duda el código de la aplicación y la velocidad de desarrollo.

**No doy el proyecto por cerrado**. Queda pendiente por ejemplo añadir un *preloader* que informe sobre el estado de la carga de datos. Para términos muy generales, por ejemplo España, o directamente si empezamos a escribir tener vinculado la petición de datos a cada evento de cambio de la caja de búsquedas, hace poco agradable la experiencia del usuario ya que tarda y no hay información del proceso.

Quiero desarrollar el acceso a los datos “geo” de cada resultado. Los datos se obtienen con otra petición de la API y al añadir información geográfica, el deseo de añadir un mapita se hace irresistible.

El código se encuentra en [GitHub](https://github.com/sigdeletras/buscacalles-cartociudad) para poder ser descargado y mejorado. Por supuesto, son totalmente bienvenidas las críticas y comentarios constructivos.

## Recursos de interés

- [Presentando Hooks](https://es.reactjs.org/docs/hooks-intro.html)
- [Referencia de la API de los Hooks](https://es.reactjs.org/docs/hooks-reference.html)

- [React Hooks, useEffect. Añadiendo funcionalidad en el ciclo de vida de nuestro componente - III](https://midu.dev/react-hooks-use-effect-funcionalidad-en-el-ciclo-vida-componentes/)
- [React Hooks: Un gran cambio se avecina](https://pablomagaz.com/blog/react-hooks-gran-cambio-se-avecina)
- [Conoce como reutilizar código con los custom hooks de React](https://ed.team/blog/conoce-como-reutilizar-codigo-con-los-custom-hooks-de-react)
- [How To Call Web APIs with the useEffect Hook in React | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-call-web-apis-with-the-useeffect-hook-in-react)
- [Custom React Hooks Make Asynchronous Data Fetching Easy (er)](https://nimblewebdeveloper.com/blog/custom-react-hooks-data-fetching)
- [Learn about data fetching with custom React hooks](https://nimblewebdeveloper.com/blog/custom-react-hooks-data-fetching)
- [Fetching Data With React Hooks and Fetch API [Beginners Guide] - DEV](https://dev.to/madara/fetching-data-with-react-hooks-and-fetch-api-beginners-guide-2ick)
- [Learn about data fetching with custom React hooks](https://nimblewebdeveloper.com/blog/custom-react-hooks-data-fetching)
- [Fetching Asynchronous Data with React Hooks](https://www.polvara.me/posts/fetching-asynchronous-data-with-react-hooks/)
- [How to Fetch Data from an API with React Hooks (React Hooks API Tutorial)](https://rapidapi.com/blog/react-hooks-fetch-data-api/)
