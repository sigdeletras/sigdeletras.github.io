---
title:  "Ver un archivo KML desde Github en Google Maps"
excerpt_separator: "<!--more-->"
comments: true
related: true
categories:
      - 2014
tags:
      - Webmapping
      - Github
      - Bases de datos geográficas
---
        
A pesar de que cada vez hay más alternativas para la publicación de datos geográficos en Internet, Google sigue llevando la voz cantante en esto del "webmapping" o mejor dicho en esto del **_"fast webmapping"_**. Con apenas cuatro "clicks" podemos incluir en nuestra página web un _mapita_ de **GoogleMap** con la situación de tu negocio, indicar el lugar de la celebración de un evento o presentar la localización de las sedes de las oficinas de atención al ciudadano de una provincia con datos asociados.

Esta inmediatez, y sin duda la popularidad de Google y de sus servicios, hace que aún teniendo una infraestructura tecnológica avanzada (GIS, Bases de datos geográficas, servicios OGC de visualización y/o descarga...) para la generación de datos geográficos en _muchas ocasiones los datos sean presentados en la Web utilizando las herramientas y servicios de GoogleMaps_.

Por experiencia, estoy comprobando que **esto está siendo muy habitual en pequeños ayuntamientos o entidades locales que desean comenzar a publicar sus geodatos, no disponen de muchos recursos humanos y tecnológicos pero sobran ganas de acercar datos a sus ciudadanos**.

Partiendo de la base de que ya tenemos la información geográfica que queremos publicar en formato KML/KMZ, voy a comentar **¿cómo publicar la información en formato KML o KMZ en GoogleMap?**

### [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-22-ver-un-archivo-kml-en-googlemaps.md#subir-los-archivos-kmlkmz-a-un-internet)Subir los archivos KML/KMZ a un Internet

En primer lugar, y tras generar/obtener el correspondiente fichero KML, debemos subir el fichero a Internet. Si tenemos a mano un servicio de alojamiento será tan fácil como subir este fichero a nuestro servidor, por ejemplo vía FTP.

Pero **¿qué ocurre si no contamos con un _hosting_ propio?**. Bueno pues en ese caso podremos subir el archivo KML/KMZ a nuestra cuenta **Dropbox*** y hacer la carpeta pública, para después obtener la URL del fichero. Otra opción es crear un Gist en [**GitHub**](https://gist.github.com/) y pegar el código del KML. Una vez hecho obtenemos la dirección del fichero pinchando en el icono _View raw_. El resultado será algo parecido a esto:

[https://gist.githubusercontent.com/pasoriano/f9835241fc017b6cb200/raw/ab268b87f6ef84ff7140261390f9fda190bf4ada/biclaspalmaswikipedia.kml](https://gist.githubusercontent.com/pasoriano/f9835241fc017b6cb200/raw/ab268b87f6ef84ff7140261390f9fda190bf4ada/biclaspalmaswikipedia.kml)

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-22-ver-un-archivo-kml-en-googlemaps.md#ver-archivos-kml-en-googlemap)Ver archivos KML en GoogleMap

Para crear el link de acceso a la visualización en GoogleMaps, añadiremos a la dirección crearemos la_[https://maps.google.com/maps](https://maps.google.com/maps)_ el parámetro de consulta mediante _?q=_ seguido de la dirección web de nuestro fichero KML/KMZ, en nuestro caso almacenado en GitHub. Podemos utilizar cualquier editor de texto y después pegarlo en el navegador o directamente usar desde el navegador.

[https://maps.google.com/maps?q=https://gist.githubusercontent.com/pasoriano/f9835241fc017b6cb200/raw/ab268b87f6ef84ff7140261390f9fda190bf4ada/biclaspalmaswikipedia.kml](https://maps.google.com/maps?q=https://gist.githubusercontent.com/pasoriano/f9835241fc017b6cb200/raw/ab268b87f6ef84ff7140261390f9fda190bf4ada/biclaspalmaswikipedia.kml)

## [](https://github.com/sigdeletras/sigdeletras.github.io/blob/master/_posts/2014/2014-05-22-ver-un-archivo-kml-en-googlemaps.md#a%C3%B1adiendo-par%C3%A1metros-a-la-consulta-googlemaps)Añadiendo parámetros a la consulta GoogleMaps

La dirección anterior es la configuración básica de nuestra consulta y el mapa resultante, pero podemos añadir una gran número de parámetros a nuestra URL en el caso de querer, por ejemplo: centrar la vista de nuestro mapa (&ll=37.957192,-4.792786), cambiar el idioma de GoogleMaps (&hl=it), asignar un nivel de zoom inicial(&z=9) o cambiar el mapa base de GoogleMaps (&t=p).

En la siguiente dirección podríamos ver la **localización de los Bienes de Interés de provincia de Las Palmas disponible en la Wikipedia, sobre la base de terreno, centrado en localización y zoom en la Isla de Gran Canaria y con GoogleMaps en inglés**.
        
