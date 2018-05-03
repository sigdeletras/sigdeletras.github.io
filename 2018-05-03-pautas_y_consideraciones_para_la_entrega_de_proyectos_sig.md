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

El objetivo de este texto se centra en definir un conjunto de pausas y consideraciones, que según mi experiencia, deben tenerse en cuenta a la hora de realizar una entrega de un proyecto de base geográfica en la que se ha usado un SIG.

Algunas de estas notas se basan en la reciente experiencia acumulada en el trabajo realizado junto a la empresa Planem Ingeniería, Arquitectura y Urbanismo S.L. En este contrato, realizado para el Ayuntamiento de Zuheros a través del Servicio Arquitectura y Urbanismo de la Diputación de Córdoba. En el estudio se trataba de **"…a partir de un análisis de distintas variables (urbanísticas, físicas, de accesibilidad, etc.), identificar las zonas del territorio aptas para acoger el parking de vehículos preferentemente turísticos; delimitar dos o más opciones de localización y, mediante la valoración de varios factores clave, jerarquizar las localizaciones en función de su idoneidad para acoger el uso pretendido usando para ello técnicas de evaluación multiciterio (EMC) usando para ello Sistemas de Información Geográfica"**.

Como parte final del proyecto, y requisito del contrato, se debían incluir en la entrega no solo la memoria del mismo, sino también los datos usados y capas geográficas resultantes en su correspondiente soporte informática.

## Software SIG

Ya que actualmente uso [QGIS](https://www.qgis.org/) para realizar mis trabajos, este artículo está principalmente orientado a la entrega de proyectos en ente SIG. Esto no quiere decir que las pautas, con algunas consideraciones, no pueda aplicarse a otros SIG de escritorio, ej. [gvSIG](http://www.gvsig.com/es). Bastaría con indicar el software que se ha utilizado y los enlaces a las páginas de descarga o, porqué no, añadir en una carpeta los ejecutables de la aplicación. En el caso de usar un programa propietario, los pasos serían los mismos, pero con la diferencia de que no podemos añadir el propio paquete informático.

## Estructura del proyecto

Para que el proyecto SIG sea cargado correctamente, toda la información: capas vectoriales, ráster, tablas, archivos de simbología, imágenes... debe estar guardados en el mismo directorio raíz que el proyecto. Podemos crear una estructura de subcarpetas donde ir organizando cada uno de los elementos del proyecto (CAPAS, RASTER , TABLAS, IMÁGENES, DOCUMENTOS...), pero siempre dentro de la carpeta del proyecto.

![Ejemplo de estructura de capas](/images/blog/201805_proyectossig/carpetas.PNG)

Teniendo habilitada la opción de "Rutas relativas" en QGIS, esta organización permitirá que al entregar la información, el sistema encuentre y cargue sin problemas los recursos del proyecto. En el caso contrario, el SIG nos avisará que no encuentra las capas en la ruta indicada y se deberá indicar la ruta de las mismas. Hay algunos complementos de QGIS para ello, como por ejemplo [Qconsolidate](http://plugins.qgis.org/plugins/qconsolidate/).

## Formatos

Hasta que no se popularice el formato [geopackage](https://www.geopackage.org/), y por mucho que les duela a muchos, los datos deberán ser guardados en formato **Shape**. Los SIG permiten trabajar en varios formatos, pero todavía, shape es el más popular. Ahora sí, este formato tiene sus [restricciones](http://switchfromshapefile.org/): archivo mutiformato, los nombres de los campos están limitados a 10 caracteres, hay un tope de su tamaño... Todo esto deberá ser tenido en cuenta, sobre todo en la fase inicial de diseño.

Para superar estas limitaciones, tenemos dos alternativas:

- Si queremos almacenar campos con más texto podemos generar un **archivo de texto (txt, csv...) o una hoja de cálculo** para guardar esta información. La tabla deberá ser cargada en el proyecto y vinculada mediante unión a la capa geométrica mediante un campo común.

- La opción más potente, y mi preferida, es la de realizar la entrega en un archivo [**SpatiaLite**](https://live.osgeo.org/es/overview/spatialite_overview.html). De esta forma, en un único archivo podremos almacenar todas las capas del proyecto, no estando limitados en el número de caracteres y con otras muchas más posibilidades que nos ofrece trabajar con una base de datos geográfica (creación de capas virtuales mediante vistas, manejo de claves primarias y foráneas, almacenamiento de tablas no geográficas, guardado de estilos...). Os dejo un enlace a la entrada titulada [Trabajando con SpatiaLite](http://www.sigdeletras.com/2014/trabajando-con-spatialite/)  que escribí hace un tiempo.

Comentar también que si nuestros datos están en una base de datos geográfica en red tipo PostGIS, deberemos transformar a algunas de estas dos opciones nuestros datos.

## Organización de capas dentro del proyecto.

Una correcta organización de las capas dentro del proyecto es fundamental. La agrupación de capas será muy útil para la poder activar/desactivar datos relacionados. Este sistema es también interesante para relacionar los datos que se presentarán en un determinado diseño de impresión. 

En los cursos que imparto suelo insistir a mis alumnos en la asignación de los nombres de los ficheros. Es recomendable usar nombres en los que no haya espacios y que sean los suficientemente ilustrativos. Yo suelo hasta incluir la fecha de referencia como prefijo, el tipo de geometría (POL, PUN o LIN) y si me apuras hasta el código EPGS que indica el sistema de referencia de coordenadas. Sin embargo, al añadir estos datos al proyecto para su presentación o entrega, es aconsejable cambiar estos nombres por textos más legibles y que identifiquen con claridad lo que representan. La equivalencia entre el nombre del fichero y el nombre de la capa dentro del proyecto deberá quedar reflejado en un documento descriptivo anexo. 

![Organizacion de capas](/images/blog/201805_proyectossig/capas.PNG)

## Estilo y simbología.

La elección de unos correctos estilos, vamos la correcta aplicación de técnicas de semiología gráfica, tanto en simbología como en etiquetado, es una labor fundamental. En este tarea incluyo también la configuración de la presentación de los datos en los formularios de identificación (uso de alias, uniones, controles tipo casilla de verificación, desplegables...). 

Todo este trabajo será accesible en nuestro proyecto pero ¿qué ocurrirá si se quiere cargas alguna de las capas en un proyecto nuevo con la misma simbología?. La solución es adjuntar al fichero de datos un archivo de configuración de estilo. La forma sencilla de hacerla es desde el formulario de Propiedades, en el botón de Estilos, usar la opción de Guardar como predeterminado. Se genera un fichero, qml o sld, con el mismo nombre de nuestra capa. Así al carga las capa en un nuevo proyecto se añadirá por defecto con el estilo adjunto. El uso de  archivos de estilos es aplicable tanto a capas vectoriales como a datos raster, incluso a tablas.

![Guardar estilos](/images/blog/201805_proyectossig/estilo.PNG)

## Diseñador de mapas para impresión.

Una vez terminado el diseño de nuestro mapa, y tras generadas las salidas gráficas (pdf, tif, svg...) mediante el Diseñador no se nos puede olvidar activar activar las opciones "Bloquear Capas" y "Bloquear Estilos para las capas". Gracias a esto, nuestros diseños quedarán "congelados" y se evitará que si se modifican los estilos posteriormente, esto afecte a nuestros diseños  y salidas gráficas entregables. Recomendable igualmente interesa desactivar la opción de “Autoactualizar” las entradas en la leyenda una vez terminada de personalizar.

![Opciones de bloque de capas en Diseñador](/images/blog/201805_proyectossig/bloqueocapas.PNG)

Por experiencia creo que es mejor generar tantos proyectos como diseños de mapas tengamos. Un proyecto con múltiples diseños tiene bastante más peso y tardará bastante en cargar. Si a pesar de esto decidimos tener varios diseños en un único proyecto de QGIS, por ejemplo para representar distintos mapas temáticos de una misma capa, será muy recomendable duplicala en el proyecto y aplicar para cada una su correspondiente simbología. 

## Documento descriptivo del proyecto y de las capas.

En ocasiones, el término metadatos puede causar cierto rechazo. Rara vez, a no ser que sea añadido en el pliego de condiciones técnicas, me he visto en la necesidad de crear los correspondientes metadatos según las ISO existentes para ello. Esto no quita para que debamos añadir a nuestra memoria o informe un sencillo informe con datos básicos de cada proyecto. 

Como información básica, este documento debe incluir:

- Sistema de referencia de coordenadas del proyecto y de las capas, sobre todo si se trabajan con varios.
- Sistema de codificación de los datos alfanuméricos. Recomendable UTF-8.
- Nombre de cada capa del proyecto y su identificación con el fichero almacenado.
- Ruta relativa del fichero
- Tipo de geometría o modelo de representación
- Breve descripción y datos básicos sobre la capa.
- En las capas que lo requieran, esto es ya para nota, conjunto de atributos y descripción de los mismos.

![Ejemplo metadatos del proyecto](/images/blog/201805_proyectossig/metas.PNG)

Como dice el refrán "cada maestrillo tiene su librillo" y mi intención es compartir mi experiencia acumulada en varios años dedicado a estos de los SIG. Seguro que se os ocurrirán muchas otras recomendaciones. Si os apetece podéis indicarlas en comentarios y podemos ir generando entre todos un documento mejorado.