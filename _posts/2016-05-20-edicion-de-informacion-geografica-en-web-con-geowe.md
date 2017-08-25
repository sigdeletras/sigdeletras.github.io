---
title:  "Edición de Información Geográfica en Web con GeoWE"
excerpt_separator: "<!--more-->"
comments: true
header:
  teaser: "/images/header/2016-05-20-geowe_catastro.png"
related: true
categories: 
       - 2016
tags:
       - GeoWE
       - Webmapping
---

Como se indica en su [página web](http://www.geowe.org/), **GeoWE**  *es un proyecto software orientado a la edición de Información Geográfica en Web, cuya culminación toma la forma de una aplicación cliente disponible para edición en diversos dispositivos. Se trata de una iniciativa de código abierto basada en el framework Google Web Toolkit (GWT), cuyo desarrollo y mantenimiento se lleva a cabo por parte de un equipo experimentado en SIG, abierto a todo el mundo a colaborar en el proyecto*.

<!--more-->

El primer contacto que tuve con el equipo GeoWe fue en el pasado [Geonquietos Córdoba](https://wiki.osgeo.org/wiki/Category:Geoinquietos_C%C3%B3rdoba) y tras comenzar a utilizar esta estupenda aplicación y conocer al magnífico [equipo](http://www.geowe.org/index.php?id=equipo) que está detrás del proyecto he de reconocer que me he convertido en un auténtico _groupie_ de GeoWE.

Tras nuestra última reunión, con café y dulzaina incluida, he decido apoyar al proyecto testeado la aplicación y [aportando](https://github.com/geowe/geowe-core/issues) los _bugs_, mejoras o comentarios que me van surgiendo.

[![](/images/blog/05_geowe/twitter.png)](https://t.co/YPhmW58EjP "merendola")

Pienso que la mejor manera de conocer GeoWE es usándolo, por lo que aquí os dejo una práctica sencilla para empezar a utilizar este SIG Web.

Por cierto, la gente de GeoWE está presentando la aplicación en las próximas [Jornadas de SIG Libre de Girona](http://www.sigte.udg.edu/jornadassiglibre/)...me han dicho que llevan camisetas;-)

## Objetivo

*   Vamos a crear una capa de tipo poligonal para dibujar unas parcelas sobre el servicio WMS de Catastro.
*   Para cada polígono recopilaremos la referencia catastral, su dirección postal y su correspondiente enlace a la Sede de Catastro.
*   Una vez obtenidos los datos con GeoWE, los salvaremos a el archivo en local para poder trabajar con el el en un SIG.

## Abrimos GeoWE

Desde nuestro pc, tablet o teléfono, podemos acceder a GeoWE en la siguiente dirección [http://demo-geowe.rhcloud.com/App.html](http://demo-geowe.rhcloud.com/App.html).

Para empezar nuestro "trabajo" lo primero que hacemos es centrar la vista del mapa a nuestra zona de interés. La herramienta **Geolocalización** que está situada en el menú superior izquierda nos permite centrar el mapa de distintas maneras.

![](/images/blog/05_geowe/24.png)

*   Localización por dirección (ej. Calle Lucano, Córdoba)
*   Utilizando el servicio [what3Words](http://what3words.com/es/). Nuestra zona de trabajo está codificada como "estará.sentí.prisa".
*   Geocoding por coordenadas (latitud/longitud) o ubicación actual.

En la barra de iconos situados a la derecha encontramos la herramienta de **"Información"** que nos informa de la capa activa, sistema de coordenadas en las que estamos trabajando, longitud y latitud y la escala . Podemos igualmente cambiar el SRC y obtener las coordenadas del punto ya que, al pinchar en una localización en el la vista del mapa, las coordenadas se quedan fijadas.

![](/images/blog/05_geowe/25_coordendas.png)

## Añadir mapas base

Nuestras parcelas van ser dibujadas sobre la capa WMS de Catastro, por lo que primero debemos cargarla para tenerla activa en nuestro Administrador de capas. Para ello accedemos a **Menú>Mapa>Catálogo** y añadimos el servicio de Catastro.

![](/images/blog/05_geowe/30_catalogo.png)

GeoWE cuenta ya con un importante número de servios de mapas en su catálogo (Google, Bing, IGN, Catastro, OSM..), pero podemos añadir nuestros otros servicios WMS desde el **Menú>Mapa>Capa>Raster** y a continuación **Añadir capa WMS**. A continuación introducimos la URL del servicio WMS, el nombre de la capa y el formato de imagen.

![](/images/blog/05_geowe/31_wms_catastro.png)

## Crear capa vectorial

Nuestra intención es dibujar una serie de manzanas catastrales con geometría de polígonos. El primer paso es generar dicha capa en GeoWE desde **Menú>Capa>Añadir**.

![](/images/blog/05_geowe/32_añadir_capa_vectorial.png)

Las opciones de **"Añadir"** son múltiples: desde cero o vacía, añadir capa desde una URL, pegar código, subir un archivo o descargar desde un servicio WFS. Los formatos disponibles de subida son GeoJSON, KML, GML y WKT.

En este caso vamos a crear una capa nueva que se llamará "parcelas_catastro", en ETRS89 UTM30N (EPSG:25830).

Podemos comprobar que nuestra capa está creada accediendo a **Menú>Capas>Vector**. Desde el "Administrador de capas" podemos:

*   Añadir/Eliminar capas.
*   Hacer [zum](http://dle.rae.es/?id=cWlLJHL) a la capa.
*   Obtener información de la capa.
*   Descargar a local en formatos GeoJSON, KML, GML, WKT y CSV.
*   Añadir y modificar los atributos.

## Dibujando geometrías

Desde **Menú>Dibujo>Polígono** seleccionaremos el tipo geográfico y empezaremos a dibujar nuestros polígonos. En este menú se encuentra también otras herramientas de edición que podemos usar para desplazar geometrías o redibujar nodos.

![](/images/blog/05_geowe/36_dibujo.png)

GeoWE permite dibujar de forma precisa activando la opción de **"Snapping"** que utiliza los nodos de geometrías existentes para ajustar las nuevas ediciones.

![](/images/blog/05_geowe/37_opciones_edicion.png)

Si queremos realizar operaciones espaciales más complejas como **uniones, divisiones, buffer**... podemos ejecutarlas desde la pestaña **"Espaciales"**.

## Añadiendo atributos

Como he indicado, la finalidad de este ejercicio es la de dibujar una serie de manzanas catastrales y obtener una serie de atributos como la referencia catastral, la dirección, el tipo de construcción, etc.

Una vez dibujadas las manzanas vamos a añadir las columnas de atributos que vamos a completar. Para ello vamos al "Administrador de capas" desde **Menú>Capas>Vector**. Tras seleccionar nuestra capa "parcelas_catastro" pinchamos en el botón **"Atributos de capa"**. En el formulario iremos añadiendo tantos atributos como queremos. Para esta capa hemos añadido tres: parcela, dirección y enlace.

![](/images/blog/05_geowe/40_atributos.png)

Para completar los datos de cada uno de los polígonos dibujados utilizaremos la opción **"Info/Edit"** de la barra **"Utilidades"** de GeoWE. A medida que vayamos pinchando en cada polígono nos aparecerá un formulario para ir completando la información de capa manzana.

Los datos podemos obtenerlos de forma visual o directamente desde Catastro usando la opción **"WMS info"**.

![](/images/blog/05_geowe/42_edicion_atributos.png)

## Salvando los datos en local.

Una vez que hemos terminado nuestra edición con GeoWE podemos exportar a local nuestra capa. Desde **Menú>Capas>Vector** seleccionamos nuestra capa y pinchamos en el botón **"Exportar"**. Una vez activa esta herramienta definimos el formato a exportar y el Sistema de Coordenadas para a continuación descarga el fichero.

Una vez almacenados en nuestro equipo ya tenemos disponible nuestra capa geográfica creada con GeoWE para poder utilizarla en el caso que queramos con nuestro SIG de cabecera.

![](/images/blog/05_geowe/42_qgis.png)
        
