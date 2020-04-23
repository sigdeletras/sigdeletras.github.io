---
title:  "Side Project: Desarrollo de aplicación web con React y Leaflet (I)"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/images/blog/202004_react_leaflet/react.png" 
categories: 
  - 2020
tags:
  - react
  - leaflet
---

Una conclusiones de mi [proyecto de fin de ciclo](http://www.sigdeletras.com/2020/presentacion-proyecto-fp-web-rutas-turisticas-node/), que presenté en enero de 2020, fue la necesidad de aprender a usar un entorno de trabajo JavaScript para la parte *front-end* de cualquier proyecto web.

> “No lo intentes. Hazlo, o no lo hagas, pero no lo intentes” — Maestro Yoda

Con este objetivo, y aprovechando los días de vacaciones, **me he propuesto aprender a usar [React](https://es.reactjs.org/)** mediante la puesta en marcha de un *Side project* personal. 

El proyecto consiste en el **desarrollando una aplicación web que permita la consulta de información temática relativa a las infraestructuras municipales (ej. saneamiento, alumbrado...) obtenidas de un [Web Feature Service (WFS)](https://es.wikipedia.org/wiki/Web_Feature_Service) público y su representación geográfica en visor de mapas**.

![react](/images/blog/202004_react_leaflet/react.png)

## ¿Porqué React?

Cualquier persona que tenga algo más de recorrido que yo en este tema, podrá rebatir o reafirmar mis sencillos argumentos. He intentado leer y documentarme sobre las **diferencias entre Angular, React y Vue**. Hay muchísima documentación de esto. Uno de los enlaces que más me ha gustado es la [comparación con otros framework](https://vuejs.org/v2/guide/comparison.html) que hace la misma gente de Vue. A pesar de todo, mis razonas son los siguientes:

Tenía claro que no iba a usar **Angular**, principalmente a pesar de su estabilidad, es el más antiguo de todos y por lo que he podido leer su aprendizaje inicial se hace bastante complicado. 

La idea inicial era **Vue**. Es el más actual, por lo visto es fácil para principiantes, bastante solicitado por empresas. Es más, asistí a un seminario organizado por el Aula de Software Libre de la UCO con la idea de poder usarlo en mi proyecto. Lamentablemente a la hora de la charla me quedó claro que usar Vue en mi proyecto no iba a ser tan rápido como pensaba. Iba a necesitar tiempo para adquirir las bases, y en esa fecha, entre el trabajo, el proyecto y la familia, era una opción inabarcable. Fue sin duda un mal momento para mi primer acercamiento a Vue.

Tras recuperar un poco de tranquilidad (lectura del proyecto) y tiempo, decidí volver a retomar mi idea. Y en esta ocasión le tocó a **React**. ¿Porqué?, pues por un par de sencillas razones. 

  - Estoy suscrito a la cuenta de Telegram de ofertas de empleo de [Manfred](https://github.com/getmanfred/offers/wiki). Tras estar pendiente durante un tiempo,  me he dado cuenta que el manejo de **React es una de las habilidades más solicitadas en las ofertas para perfiles front-end**. Así de simple.
  - Justo antes del confinamiento, participé como ponente en las II Jornadas de Informática del IES Trassierra. Antes de mi [Taller de iniciación Node](https://medium.com/@pasoriano/taller-creando-una-api-rest-con-node-js-y-mongodb-be606121389a), estuve en varias charlas y asistí a una de React. **Me gustó, comprendí de forma rápida su funcionamiento básico y me picó la curiosidad**. Otro argumento demoledor.

## ¿Qués es React?

Todo lo que aquí pueda poner es copiado de la documentación oficial de esta librería de JavaScript, así que directamente me remito a las miles de páginas sobre este tema. Solo voy a copiar/pegar la definición en la Wikipedia que me parece sencilla y fácil comprender.

> *"React (también llamada React.js o ReactJS) es una biblioteca JavaScript de código abierto diseñada para crear interfaces de usuario con el objetivo de facilitar el desarrollo de aplicaciones en una sola página. Es mantenido por Facebook y la comunidad de software libre. Han participado en el proyecto más de mil desarrolladores diferentes."* [Wikipedia](https://es.wikipedia.org/wiki/React)

## Conceptos básicos

A pesar de que estoy totalmente de acuerdo con la **metodología *learning by doing***, para mi es fundamental comenzar con la adquisición y comprensión de los conceptos básicos necesarios para empezar a aprender cualquier tecnología. 

Esta fase es siempre complicada y suele terminar cuando encuentras esa **página "llave" a partir de la cuál uno empieza a entender mejor todo lo que anteriormente ha leído**. En esta ocasión, la página fue el  [Tutorial de React de W3Schools](https://www.w3schools.com/REACT/default.asp). 

Siguiendo este tutorial, los conceptos esenciales que creo se deben tener claros son:

- ¿Qué es un componente? Componentes funcionales (function component) y de clase (class component)
- ¿Qué son las Props y el State y cuándo se usan?
- Renderizado de HTML y uso de JSX (JavaScript + XML).
- El ciclo de vida (lifecicle) de un componente React..esto todavía me cuesta :-(
- React Events.

También es fundamental [manejarse con aspectos de ES6](http://es6-features.org/#Constants) como el uso de clases (constructor, métodos, herencia...), tipos de variables y funciones de tipo flecha.

Para completar, dejo también este enlace a un documento recomendado en la web de React y que me gustó, [Getting Started with React - An Overview and Walkthrough Tutorial](https://www.taniarascia.com/getting-started-with-react/).

## Características del proyecto

Voy a crear un documento de alcance del proyecto, para intentar ajustarme al máximo a él y no perder el tiempo.

### Descripción del proyecto

El proyecto consiste en realizar una aplicación web que permita consultar información temática relativa a las infraestructuras municipales (saneamiento, alumbrado, electricidad) y su representación geográfica en un mapa.

También forma parte fundamental generar la documentación del proyecto, que se traducirá en dos o tres entradas en mi web SIGdeletras y en Medium.

### Funcionalidades

- Selección de municipio (como mínimo 3 municipios)
- Adquisición de datos de la API (Capa de un servicio WFS, ej. alumbrado)
- Representación de datos un mapa (tipo puntual)
- Consulta de datos en mapa (popups)
- Consulta de datos en listado (tabla)
- Cambio de municipio y actualización (mapa y listado)

### Tecnología

- Librería React (Node, npm, create-react-app)
- Leaflet a través del paquete React-Leaflet
- Bootstrap como framework CSS
- Visual Studio Code

### Fases

- Recopilación básica de recursos
- Diseño de funcionalidades básicas (tareas)
- Despliegue de  infraestructura tecnológica
- Desarrollo
- Producto final (Subida a GitHub)

### Gestión de proyecto Trello

Usaré Trello, con un kanban sencillo para gestionar las tareas del tipo (*ToDO- Doing-Done*).

Por ahora tengo documentadas 18 tareas organizadas en 5 épicas (por llamarlas de alguna forma): Instalación, Diseño, Desarrollo, Testeo y Documentación.

### Plazo

Tres semanas (después familia, trabajo, casa...). Me gustaría tener contabilizadas las horas, pero ya voy tarde sobre todo el tiempo dedicado a la recopilación de recursos y enlaces.

## Documentación

El primer documento es este mismo enlace y la documentación recopilada está en este [repositorio de React & Maps de GitHub](https://github.com/sigdeletras/react_maps/blob/master/README.md).
