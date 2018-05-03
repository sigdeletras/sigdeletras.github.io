---
title:  "Pautas y consideraciones para la entrega de proyectos SIG"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201805_proyectossig/metas.PNG"
categories: 
  - 2018
tags:
  - Consultoría geográfica
---


Tras un largo tiempo sin escribir en el blog, debido al volumen de trabajo reciente del que espero poder dar cuenta en breve, voy a realizar una entrada sobre un tema muy específico pero que creo que puede ser de utilidad para aquellas empresas y profesionales que trabajan con Sistemas de Información Geográfica. 

**El objetivo de este texto se centra en definir un conjunto de pausas y consideraciones, que según mi experiencia, deben tenerse en cuenta a la hora de realizar una entrega de un proyecto de base geográfica en el que se ha usado un SIG**.

Algunas de estas notas se basan en la reciente experiencia acumulada en el trabajo realizado junto a la empresa [Planem Ingeniería, Arquitectura y Urbanismo S.L](https://www.linkedin.com/company/planem-ingenier-a-arquitectura-y-urbanismo?originalSubdomain=es). El contrato, realizado para el Ayuntamiento de Zuheros a través del Servicio Arquitectura y Urbanismo de la Diputación de Córdoba, trataba de *"…a partir de un análisis de distintas variables (urbanísticas, físicas, de accesibilidad, etc.), identificar las zonas del territorio aptas para acoger el parking de vehículos preferentemente turísticos; delimitar dos o más opciones de localización y, mediante la valoración de varios factores clave, jerarquizar las localizaciones en función de su idoneidad para acoger el uso pretendido usando para ello técnicas de evaluación multiciterio (EMC) usando para ello Sistemas de Información Geográfica"*.

Como parte final del proyecto, y requisito del contrato, se debía incluir en la entrega no solo la memoria del mismo, sino también los datos usados y capas geográficas resultantes en su correspondiente soporte informático.

## Software SIG

Ya que actualmente uso [QGIS](https://www.qgis.org/) para realizar mis trabajos, este artículo está principalmente orientado a la entrega de proyectos con este programa. Esto no quiere decir que las pautas, con algunas consideraciones, no pueda aplicarse a otros SIG de escritorio como por ejemplo [gvSIG](http://www.gvsig.com/es). Bastaría con **indicar el software que se ha utilizado y los enlaces a las páginas de descarga**, o porqué no, añadir en una carpeta los ejecutables de la aplicación (recuerden las [4 libertades del software libre](https://es.wikipedia.org/wiki/Software_libre#Las_cuatro_libertades_del_software_libre)). En el caso de usar un SIG propietario, los pasos serían los mismos, pero con la diferencia de que no podemos distribuir copias del programa.

## Estructura del proyecto

Para que el proyecto SIG sea cargado correctamente, **toda la información: capas vectoriales, ráster, tablas, archivos de simbología, imágenes... debe estar guardados en el mismo directorio raíz que el proyecto**. Podemos crear una estructura de subcarpetas donde ir organizando cada uno de los elementos del proyecto (CAPAS, RASTER , TABLAS, IMÁGENES, DOCUMENTOS...), pero siempre dentro de la carpeta del proyecto.

![Ejemplo de estructura de capas](/images/blog/201805_proyectossig/carpetas.PNG)

Teniendo habilitada la opción de ***"Rutas relativas"*** en QGIS, esta organización permitirá que al entregar la información, el sistema encuentre y cargue sin problemas los recursos del proyecto. En el caso contrario, el SIG nos avisará que no encuentra las capas en la ruta indicada y se deberá indicar la ubicación de los ficheros, eso si, siempre que no se nos haya olvidado entregarlos ;-). Hay algunos complementos de QGIS para ello, véase por ejemplo [Qconsolidate](http://plugins.qgis.org/plugins/qconsolidate/).

## Formatos

Hasta que no se popularice el formato [geopackage](https://www.geopackage.org/), los datos **deberán ser guardados en formato *shape***. Los SIG permiten trabajar en varios formatos, pero todavía shape sigue siendo el más popular o al menos el más indicado como formato de entrega. Ahora sí, este formato tiene sus [restricciones](http://switchfromshapefile.org/): archivo mutiformato, los nombres de los campos están limitados a 10 caracteres, hay un tope de su tamaño, no se puede añader más de 255 caracteres... Todo esto deberá ser tenido en cuenta, sobre todo en la fase inicial de nuestro trabajo e igualmente, por los técnicos redactores de los pliegos.

Para superar estas limitaciones, tenemos dos alternativas:

- Si queremos almacenar campos con más texto podemos generar un **archivo de texto (txt, csv...) o una hoja de cálculo** para guardar esta información. La tabla deberá ser cargada en el proyecto y vinculada mediante unión a la capa geométrica mediante un campo común.

- La opción más potente, y mi preferida, es la de realizar la entrega en un archivo [**SpatiaLite**](https://live.osgeo.org/es/overview/spatialite_overview.html). De esta forma, en un único archivo podremos almacenar todas las capas del proyecto, no estando limitados en el número de caracteres y con otras muchas más posibilidades que nos ofrece trabajar con una base de datos geográfica (creación de capas virtuales mediante vistas, manejo de claves primarias y foráneas, almacenamiento de tablas no geográficas, guardado de estilos...). Os dejo un enlace a la entrada titulada [Trabajando con SpatiaLite](http://www.sigdeletras.com/2014/trabajando-con-spatialite/) que escribí hace un tiempo.

Comentar también que si nuestros datos están en una base de datos geográfica en red tipo PostGIS, deberemos transformar a algunas de estas dos opciones nuestros datos.

## Organización de capas dentro del proyecto.

Una correcta organización de las capas dentro del proyecto es fundamental. La **agrupación de capas** será muy útil para la poder activar/desactivar datos relacionados en las vistas. Este sistema es también interesante para relacionar los datos que se presentarán en los diseños de impresión. 

En los cursos que imparto suelo insistir a mis alumnos en la asignación de los nombres de los ficheros. Es recomendable usar nombres en los que no haya espacios, ni tildes y que sean los suficientemente ilustrativos. Yo suelo añadir la fecha de creación como prefijo, el tipo de geometría (POL, PUN o LIN) y si me apuráis hasta el código EPGS, aunque siempre incluya el correspondiente archivo *proj*. Sin embargo, al añadir estos datos al proyecto para su presentación o entrega, **es aconsejable modificar estos nombres por textos más legibles** y que identifiquen con claridad lo que representan en el árbol de capas. La equivalencia entre el nombre del fichero SIG y el nombre de la capa QGIS deberá quedar reflejado en un documento descriptivo anexo. 

![Organizacion de capas](/images/blog/201805_proyectossig/capas.PNG)

## Estilo y simbología.

La elección de unos  estilos de representación adecuados, vamos la correcta aplicación de técnicas de semiología gráfica, tanto en simbología como en etiquetado, es una labor fundamental. En este tarea incluyo también la configuración de los formuarios de identificación: uso de alias,  controles tipo casilla de verificación, desplegables, uniones...). 

Todo este trabajo será accesible en nuestro proyecto pero ¿qué ocurrirá si se quiere cargar alguna de las capas on la misma simbología en un proyecto nuevo?. La solución es **adjuntar al fichero SIG el archivo de configuración de estilo**. La forma sencilla de crearlo es desde el formulario *Propiedades* de la capa, en el botón de *Estilos*, usando la opción de *Guardar como predeterminado*. Se genera un fichero, qml o sld, con el mismo nombre de nuestra capa. Así al carga las capa en un nuevo proyecto se añadirá por defecto con el estilo adjunto. El uso de  archivos de estilos es aplicable tanto a capas vectoriales como a datos raster, incluso a tablas.

![Guardar estilos](/images/blog/201805_proyectossig/estilo.PNG)

## Diseñador de mapas para impresión.

Una vez terminado el diseño de nuestro mapa, y tras generadas las salidas gráficas (pdf, tif, svg...) mediante el *Diseñador* no se nos puede olvidar activar **activar las opciones *"Bloquear Capas" y "Bloquear Estilos para las capas"***. Gracias a esto, nuestros diseños quedarán "congelados" y se evitará que si se modifican los estilos posteriormente, esto afecte a nuestros diseños  y salidas gráficas entregables. Recomendable igualmente interesa desactivar la opción de ***“Autoactualizar”* las entradas en la leyenda** una vez terminada de personalizar.

![Opciones de bloque de capas en Diseñador](/images/blog/201805_proyectossig/bloqueocapas.PNG)

Por experiencia creo que **es mejor generar tantos proyectos como diseños de mapas tengamos**. Un proyecto con múltiples diseños tiene bastante más peso y tardará bastante en cargar. Si a pesar de esto decidimos tener varios diseños en un único proyecto de QGIS, por ejemplo para representar distintos mapas temáticos de una misma capa, será muy recomendable duplicala en el proyecto y aplicar para cada una su correspondiente simbología. 

## Documento descriptivo del proyecto y de las capas.

En ocasiones, el término metadatos puede causar cierto rechazo. Rara vez, a no ser que sea requerido en el pliego de condiciones técnicas, me he visto en la necesidad de crear los correspondientes metadatos según las ISO existentes para ello. Esto no quita para que debamos **añadir a nuestra memoria o informe un sencillo informe con datos básicos de cada proyecto y sus capas**. 

Como información básica, este documento debe incluir:

- Sistema de referencia de coordenadas del proyecto y de las capas, sobre todo si se trabajan con varios.
- Sistema de codificación de los datos alfanuméricos. Recomendable UTF-8.
- Nombre de cada capa del proyecto y su identificación con el fichero almacenado.
- Ruta relativa del fichero
- Tipo de geometría o modelo de representación
- Breve descripción y datos básicos sobre la capa.
- En las capas que lo requieran, esto es ya para nota, conjunto de atributos y descripción de los mismos.

![Ejemplo metadatos del proyecto](/images/blog/201805_proyectossig/metas.PNG)

# CADA MAESTRILLO...

Como dice el refrán "cada maestrillo tiene su librillo" y mi intención es compartir mi experiencia acumulada en varios años dedicado a estos de los SIG. Seguro que se os ocurrirán muchas otras recomendaciones. Si os apetece podéis indicarlas en comentarios y podemos ir generando entre todos un documento mejorado.
