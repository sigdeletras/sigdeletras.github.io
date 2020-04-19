---
title:  "Side Project: Desarrollo de aplicación web con React y Leaflet (II). Creando componentes"
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


## Creando la aplicación baśica con Create React App

Como primera tarea dentro de este **side project personal**, que tiene como **objetivo adquirir los conocimientos básicos de la librería [React](https://reactjs.org/)**, encuentra el tema de la instalación. 

Lo más frecuente para empezar un proyecto React, al menos para alguien que está empezando, es usar [Create React App](https://create-react-app.dev/docs/getting-started/). Esta herramienta es un CLI oficial que nos va a instalar las librerías y crear la estructura básica para una aplicación de una única página (single-page application o SPA). 

**La idea de un *side project* es poder completar con éxito nuestro proyecto y centrarnos al máximo en nuestro objetivo**. Es por ello recomendable usar las herramiemtas disponibles que agilicen el trabajo. No pararme ahora en  ver cómo realziar todo el despliegue de una aplicación (instalación, paquetizado, transpilación...). Solo me interesa centrarme en Reat y usar CRA me parece una idea acertada.

La [documentación](https://create-react-app.dev/) es bastante completa, así que no entraré en detalles de como usarlo. Para crear la aplicación ejecutamos siguiente comando:

```
npx create-react-app geoapp
cd geoapp
```

Usamos el script *start* que viene definido en *package.json* y levantamos nuestro servidor de desarrollo.

## Instalación de librerías: Leaflet, React-Leaflet y Boostrap

Usamos  el gestor de paquetes [nmp](https://www.npmjs.com/) para añadir las librerías de mapas. [Leaflet](https://leafletjs.com/) será el paquete de base nuestro visor web, donde representaremos los datos geográficos que obtendremos de un servicio WFS, en su contexto geográfico. 

Siguiendo con la filosofía de "no reinventar la rueda" instalaremos también [React-Leaflet](https://react-leaflet.js.org/en/) que crea componentes React a partir de las clases de Leaflet.

```
npm install -S leaflet react-leaflet
```

Terminamos las instalaciones añadiendo **Bootstrap** como *framework* CSS.

```
npm install -S bootstrap
```

Añadiremos al fichero en  *index.js*, tal y como indica la [documentación de CRA](https://create-react-app.dev/docs/adding-bootstrap/).

![Bootstrap](/images/blog/202004_react_leaflet_2/2_add_bootstrap.png)

## Depurando archivos de CRA

Antes de empezar a crear nuestros componentes, creo oportuno limpiar el código y eliminar los archivos que no vamos a usar del proyecto creado por CRA. He eliminado el código de la función App dentro del archivo *App.js* (archivo principal de la aplicación). También he quitado el código CSS y algún archivo SVG.


## Componentes funcionales - Componentes de clase

Una de los primeros conceptos de React que he tenido que aprender ha consistido en las distintas formas que existen para crear Componentes. **Los componentes React puede crear mediante una función o una clase**.

El siguiente ejemplo crea componente mediente una función JS (**componente funcional**) que devuelve un elemento H1.

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Si usamos clases ES6,  extendiendo desde  *React.Component*  y usando el método *render()* de React para devolver el elemento, creamos un componente de clase cuyo código quedaría así.

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
Los dos **son equivalentes**, y ambos devuelven código JSX. En mi proyecto **voy crear lo componentes como clases** porque ahora mismo me resulta más entendible (seguro que hay mejores razones técnias...)

He añadido código de ejemplo dentro del componente principal App. Este será el que posteriormente me sirva para definir los componentes hijos. Con esto, el código del componente principal quedará así en el fichero *App.js*, una vez definida la rejilla básica de la página con Bootstrap. 


```javascript
//App.js
import React from 'react';

import './App.css';

class App extends React.Component {

  render() {
    return (
      <div className="container-fluid">
        <div className="row m-3">
          <div className="col-12">
            <h1 className="text-center">GeoApp</h1>
          </div>
        </div>
        <div className="row m-3">
          <div className="col-sm-4 col-md-2">

            <div class="form-group">
              <label for="FormControlSelect1">Municipality</label>
              <select class="form-control" id="eFormControlSelect1">
                <option>Montoro</option>
                <option>Lucena</option>

              </select>
            </div>
            <button className="btn btn-primary mb-3">Load</button>
          </div>
          <div id="map" className="col-sm-8 col-sm-offset-4 col-md-10 col-md-offset-3">
          </div>
        </div>
        <div className="row m-3">
          <div className="col">
            <table className="table table-striped">
              <thead>
                <tr>
                  <th>ID</th>
                  <th>Type</th>
                  <th>Name</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>1</td>
                  <td>Type 1</td>
                  <td>name 1</td>
                </tr>
                <tr>
                  <td>2</td>
                  <td>Type 2</td>
                  <td>name 2</td>
                </tr>
                <tr>
                  <td>3</td>
                  <td>Type 1</td>
                  <td>name 3</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    )
  }
}
export default App;

```

![03_grid_desktop.png](/images/blog/202004_react_leaflet_2/03_grid_desktop.png)

## Componente *MapView*

El primer componente será el mapa. La documentación y ejemplos que he consultado recomientan crear una **carpeta */components* que contendrá el código de cada nuevo componente**. Para una mejor organización, y pensando que voy a crear tres componentes, añadiré para cada uno su correspondiente subcarpeta, ya que en ella además del código Javascript puede guardarse el archivo CSS asociado, datos necesarios...

El archivo principal del componente MapView (*MapView.js*) debe incluir la importación de React. Debemos también añadir los componentes de Leaflet desde React-Leaflet. Concretamente vamos a necesitar el objeto [Map](https://leafletjs.com/reference-1.6.0.html#map-example) de la API de Leaflet y un [TileLayer](https://leafletjs.com/reference-1.6.0.html#tilelayer) para la capa base. Terminado con las importaciones añidiendo el CSS de Leaflet.

He creado el componente como una clase. Dentro de él se ecuentran los componentes de *Map* y *TileLayer*, a los que se les pasan determinadas propiedades a modo de parámetros (zoom, center) con síntasis JSX, usando llaves.

```javascript
//MapView.js
import React from "react";
import { Map, TileLayer } from "react-leaflet";
import "leaflet/dist/leaflet.css";

class MapView extends React.Component {
  render() {
    const styleMap = { "width": "100%", "height": "60vh" }
    return (
      <Map
        style={styleMap}
        center={[37.885963680860755, -4.774589538574219,]}
        zoom={12}>

        <TileLayer
          url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
          attribution="&copy; <a href=&quot;http://osm.org/copyright&quot;>OpenStreetMap</a> contributors"
        />
      </Map>
    )
  }

}

export default MapView;
```

Hay varias **formas de pasar CSS** a nuestro componente. La más sencilla es la que usa el atributo *style*. En vez de meter el código dentro, he creado una variable con los datos. Podemos también añadir el código en un fichero CSS dentro de la carpeta del componente.

Para terminar, comentar que he visto algunos manuales en los que el CSS puede estar definido dentro de una función. Esto permite por ejemplo añadir condicionales ternarios para evaluar estados o propiedades del componente y cambiar el CSS a estos.

## Añadiendo el compomente *MapView* a *App.js*

Creado el componente, el siguiente paso es añadirlo a nuestro componente padre *App*. Debemos importar el componente, apuntando correctamente a su ubicación dentro del árbol de carpeta del proyecto.

```javascript
// App.js
import React from 'react';
import MapView from './components/MapView/MapView.js'
...
```
Ya dentro de la clase *App*, añadimos nuestro componente. El componente se añade como un elemento HTML, en la posición correcta dentro de nuetro *grid*.

![04_mapview.png](/images/blog/202004_react_leaflet_2/04_mapview.png)

...y Voalà!

![05_mapview_in_app.png](/images/blog/202004_react_leaflet_2/05_mapview_in_app.png)

## Componente *SelectList*

El siguiente componente será un elemento HTML de tipo *select*. Las opciones de este listado van a ser cargadas desde un objeto que incluya el nombre del munipipio y que almacene las coordenadas del centro del municipio.  Los datos seleccionados deberán servir para centrar la vista del mapa y a su vez para realizar la petición de datos al servicio WFS...pero eso lo dejaremos para otro *sprint*.

Creamos el nuevo componente dentro de */components* que vamos a llamar *SelectList*. Para empezar vamos a cortar el código JSX de este elemento del archivo *App.js* y lo pegaremos dentro del componente.

```javascript
//SelectList.js
import React from 'react'

class SelectList extends React.Component {

    render() {
        return (
            <div>
                <label>Municipality</label>
                <select className="form-control">
                    <option>Montoro</option>
                    <option>Lucena</option>
                </select>
            </div>
        )
    }
}
export default SelectList;
```

Tras guardar los cambios del nuevo fichero, ahora debemos importarlo en *App.js* para poder usarlo y añadir el componente donde antes teníamos el código cortado.

```javascript
//App.js
import React from 'react';
import MapView from './components/MapView/MapView.js'
import SelectList from './components/SelectList/SelectList.js';
....

```

![06_selectlist.png](/images/blog/202004_react_leaflet_2/06_selectlist.png)

## Añadiendo opciones en *SelectList* mediante la función *map()*

Los datos del listado van a proceder de un objeto JSON. Dentro de la carpeta del componente, he creado el archivo *municipalities.json* y lo importaremos dentro de *SelectList.js*.

Los componetes de React tiene dos objetos, **state y props**, con información que influirá en el estado del render. Según la documentación oficial **"props se pasa al componente (similar a los parámetros de una función) mientras que state se administra dentro del componente (similar a las variables declaradas dentro de una función).**

Quizás quede más claro entender directamente que en *state* se guarda el estado del componente. También es importante saber que si cambiamos los valores de *state* el componente se "actualizará". Por ejemplo, si nuestro componente *MapView*, tiene dentro de su estado un valor con un array de coordenadas de las que depende el punto central de visualización, y creamos una función que modifique este valor del estado al hacer un clic, el renderizado del mapa cambiará, por lo que se habrá realiza un desplazamiento del mapa.

Voy a usar *state* para añadir un valor que almacene los datos de un objeto JSON. Este JSON tiene valores que quiero que se usen para las opciones de la lista de selección. El archivo *municipalities.json* lo he guardado en una subcarpeta dentro de la carpeta componente *SelectList*. Para usarlo la importo en el js.

![07_json.png](/images/blog/202004_react_leaflet_2/07_json.png)

Dentro de la clase creo un nuevo valor para *state* denominado *data*. Aquí vamos a almacenar este objeto.

```javascript
//SelectList.js

import React from 'react'
import municipalities from './data/ municipalities.json'

class SelectList extends React.Component {

    state = {
        data: municipalities,
    }
...

```

Ahora toca renderizar los valores de *option* de nuestra lista con los del valor *data*. Vuelvo a recurrir a los ejemplos vistos y en esta ocasión se suele usar el **método *map()***. Este método nos devuelve un array nuevo como resultado de pasar una función al array al que es llamado. En el proyecto nos devolverá un array de *options* con los parámetros obtenidos del *data* definido en el estado del elemento.

Lo primero que vamos a hacer es crear una constante que almacene la información de *state* dentro de *render()*. Aprovechamos para ello la opción de **desestructuración de ES6**.

Para terminar, añadimos el método *map* sobre este array.

```javascript
//SelectList.js
...
    render() {
        const { data } = this.state;
        return (
            <div>
                <label>Municipality</label>
                <select
                    className="form-control">
                    <option value="">Selecciona un municipio</option>
                    {data.map((m) =>
                        <option key={m.id} value={[m.coordinates, m.name]}>{m.name}</option>
                    )}
                </select>
            </div>
        )
    }
...

```

Guardados los cambios y si accedemos a las herramientas de desarrollador del navegador podremos ver el código HTML renderizado.

![08_options_select_map.png](/images/blog/202004_react_leaflet_2/08_options_select_map.png)

## Resumen de tareas realizadas en el Sprint #1

![00_01_sprint.png](/images/blog/202004_react_leaflet_2/00_01_sprint.png)

## Hilo de entradas

- [Side Project: Desarrollo de aplicación web con React y Leaflet (I)](http://www.sigdeletras.com/2020/side-project-desarrollo-de-aplicacion-web-con-react-y-leaflet-i/)

## Enlaces 

- Repositorio GitHub [React & Maps](https://github.com/sigdeletras/react_maps) (rama *master*)
