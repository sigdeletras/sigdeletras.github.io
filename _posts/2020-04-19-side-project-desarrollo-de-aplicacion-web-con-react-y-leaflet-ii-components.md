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

Como primera tarea dentro de side proyect personal que tiene como objetivo adquirir los conocimientos básicos de la librería React encuentra el tema de la instalación. 

Lo más frecuente para empezar un proyecto React, al menos para alguien que está empezando es usar [Create React App](https://create-react-app.dev/docs/getting-started/) un CLI oficial que nos va a instalar las librerías y crear la estructura básica para una aplicación de una única página (single-page application o SPA). La idea de un side project es poder completar con éxito nuestro proyecto y centrarnos al máximo en nuestro objetivo. Es por ello recomendable usar la sherramiemtas disponibles para ello y que agilicen el trabajo. En esta ocacisión no quiero ver como realziar todo el despliegue de una aplicación (instalación, paquetizado, transpilación...) solo me interesa centrarme en Reat. Es por ello que el usos de CRA me parece una idea acertada.

La documentación es bastante completa, así que no entraré en detalles de como usarlo

Una vez instalado, ejecutamos el comando

```
npx create-react-app geoapp
cd geoapp
```

Usamos el script *start* que viene definido en package.json y levantamos nuestro servidor de prueba

```
npm start
```

![React con CRA]()

Siguiendo con las instalaciones vamos a usar nmp para añadir las librerías de mapas. [Leaflet](https://leafletjs.com/) será el paquete de base nuestro visor de mapas we, donde queremos representar los datos geográficos que obtendremos de un servicio WFS. Siguiendo con la filosofía de no reinventar la rueda, al menos por ahora, instalaremos también [React-Leaflet](https://react-leaflet.js.org/en/) que crear componentes React a partir de las clasese de Leaflet.

```
npm install -S leaflet react-leaflet
```

Terminamos las instalaciones instalando [Bootstrap] como *framework* CSS

```
npm install -S bootstrap
```
Que añadiremos al fichero index.js, tal y como está definido en la [documentación de CRA](https://create-react-app.dev/docs/adding-bootstrap/).

![Bootstrap](images/blog/images/blog/202004_react_leaflet_2/2_add_bootstrap.png)


## Depurando archivos de CRA

Antes de crear nuestros componentes creo oportuno limpiar el código y eliminar los archivos que no vamos a usar del proyecto de ejemplo creado por CRA. En este trabajo he eleiminado el código de la función App dentro del archivo App.js (archivo principal de la aplicación). También he quitado el código CSS y algún archivo SVG.


## Funciones de clase o 

Una de los primeros conceptos de React que he tenido que aprender ha cosnsistido en las distintas formas que existen para crear Componentes.

Los componentes puede crear medinate una función o una clase.

Un ejemplo de un componente creado mediente una función JS que devuelve un elemento H1 es el siguiente:

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

Mientras que si usamos clases ES6,  extendiendo desde  *React.Component*  y usando la función render() para devolver el elemento.

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
Los dos son equivalentes, y ambos devuelven código JSX. En el proyecto voy usar clases más que nada porque veo con más claridad el tema de las propiedades y los estados de los componentes. 

Con esto, el código de nuestro componente principal quedará así en el fichero *App.js*, una vez definida la rejilla básica de la página con Bootstrap. He añadido código de ejemplo dentro del componente principal App. Este será el que posteriormente me sirva para definir los componentes hijos.

```javascript
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


![03_grid_desktop.png](/images/blog/images/blog/202004_react_leaflet_2/03_grid_desktop.png)

## Componente MapView

Vamos a crear nuestro primer componente que será el mapa en sí. La documentación y ejemplos que he consultado recomientan crear una carpeta */components* que contendrá el código de cada nuevo componente. Para una mejor organizacización y pensando que voy a crear tres componentes crearé para cada uno su correspondiente subcarpeta, ya que en ella además del código javascript puede guardarse el archivo CSS asociado.

El archivo principal del componente MapView (MapView.js) debe incluir importación de React. Debemos importar los componentes de Leaflet desde React-Leaflet y concretamente el que permite añadir un  objeto Map de Leaflet y un TileLayer con el mapa base. Terminado con las importaciones añidimos el css de Leaflet.

He creado el componente como una clase. Dentro de él se ecuentran los componentes de Map y TileLayer, a los que se les pasan determinadas propiedades a modo de parámetros (zoom, center) con síntasis JXS, usando que principalmente se caracteriza por usar llaves.

```javascript
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

Hay varias formas de pasar CSS a nuestro componente. La más sencilla, que es la que he usado por ahora es la que usa el atributo *style*. En vez de meter el código dentro, he creado una variables con los datos. Podemos también añadir el código en un fichero CSS dentro de la carpeta de del componente. Para terminar, comentar que he visto algunos manuales en los que el css está definido dentro de una función. Esto permite por ejemplo añadir condicionales ternarios para evaluare estados o propiedades del componente cambiar el CSS a estos.

## Añadiendo el compomente MapView a App.js

Creado el componente, el siguiente paso es añadirlo a nuestro componente padre *App*.

En primer lugar debemos importar el componente, apuntando correctamente a su ubicación dentro del 
árbol de carpeta del proyecto.

```javascript
// App.js
import React from 'react';
import MapView from './components/MapView/MapView.js'
...
```
Ya dentro de la clase App, añadimos nuestro componente. El componente se añade como un elemento HTML, en la posición correcta dentro de nuetro grid.

![04_mapview.png](/images/blog/images/blog/202004_react_leaflet_2/04_mapview.png)

...y Voalà!

![05_mapview_in_app.png](/images/blog/images/blog/202004_react_leaflet_2/05_mapview_in_app.png)

# Componente *SelectList*

El siguiente componente será un elemento HTML de tipo *select*. Las opciones de este listado van a ser cargadas desde un objeto que incluya el nombre del munipipio y que almacene las coordenadas del centro del municipio.  Los datos seleccionados deberán servir para centrar la vista del mapa y a su vez para realizar la petición de datos al servicio WFS..pero eso para otro *sprint*.

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

Tras guardar los cambios del nuevo fichero, ahora debemos importarlo en App.js para poder usarlo y añadir el componente donde antes teníamos el código cortado.

```javascript
//App.js
import React from 'react';
import MapView from './components/MapView/MapView.js'
import SelectList from './components/SelectList/SelectList.js';
....

```

![06_selectlist.png](/images/blog/images/blog/202004_react_leaflet_2/06_selectlist.png)

## Añadiendo opciones en SelectList mediante la función map()

Los datos del listado van a proceder de un objeto JSON. Dentro de la carpeta del componente, he creado el archivo *municipalities.json* y lo importaremos dentro de *SelectList.js*.

Los componetes de React tiene dos objetos, state y props, con información que influirá en el estado del render. Según la documentación oficial *"props se pasa al componente (similar a los parámetros de una función) mientras que state se administra dentro del componente (similar a las variables declaradas dentro de una función).*

Quizás quede más claro entender directamente que en *state* se guarda el estado del componente. Y también es importante saber que si cambiamos los valores de *state* el componente se "actualizará". Por ejemplo si nuestro componente MapView, tiene dentro de su estado un valor con un array de coordenadas de las que depende el punto central de visualización, y creamos una función que modifique este valor del estado al hacer un clic, el renderizado del mapa cambiará, por lo que se habrá realiza un desplazamiento del mapa.

Voy a usar *state* para añadir un valor que almacene los datos de un JSON. Este JSON tiene datos que quiero que se usen para las opciones de la lista de selección. El archivo *municipalities.json* lo he guardado en una subcarpeta dentro del componente y para usarlo la importo.

![07_json.png](/images/blog/images/blog/202004_react_leaflet_2/07_json.png)

Dentro de la clase creo un nuevo valor para *state* denominado *data* que va a almacenar este objeto.

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

Ahora toca renderizar los valores de *option* de nuestra lista con los del valor *data*. Vuelvo a recorrir a los ejemplos vistos y en esta ocasión se suele usar el método map(). Este método nos devuelve un array nuevo como resultado de pasar función al array al que es llamado. Para nuestro ejemplo nos devolverá un array de *options* con los parámetros obtenidos del valor (array) *data* definido en el estado del elemento.

Lo primero que vamos a hacer es crear una constante dentro de *render()* y aprovechar la opción de desestructuración de ES6, almacene la información de *state*.

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

![08_options_select_map.png](/images/blog/images/blog/202004_react_leaflet_2/08_options_select_map.png)

# Resumen de tareas del Sprint #1

![00_01_sprint.png](/images/blog/images/blog/202004_react_leaflet_2/00_01_sprint.png)

# Hilo de entradas

- [Side Project: Desarrollo de aplicación web con React y Leaflet (I)](http://www.sigdeletras.com/2020/side-project-desarrollo-de-aplicacion-web-con-react-y-leaflet-i/)

# Enlaces 

- Repositorio GitHub [React & Maps](https://github.com/sigdeletras/react_maps) (rama *master*)