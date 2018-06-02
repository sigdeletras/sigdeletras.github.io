---
title:  "Algunas notas sobre el geowebinar de entregas de proyectos SIG"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201805_notas_geowebinar/youtube.PNG" 
categories: 
  - 2018
tags:
  - SIG
  - geowebinar
---

Hace ya un par de semanas que tuvo lugar el [primer geowebinar organizado desde SIGdeletras](http://www.sigdeletras.com/2018/geowebinar_pautas_y_consideraciones_b%C3%A1sicas_para_la_entrega_de_proyectos_sig/) en la que varios profesionales del sector geo de España tuvimos la oportunidad de debatir y compartir experiencias sobre aspectos vinculados con la entrega de proyectos realizados con SIG. Por si alguno no pudo asistir o tiene ganas de verlo completo se encuentra accesible en YouTube desde la dirección [http://bit.ly/sigdeletras_geowebinar](http://bit.ly/sigdeletras_geowebinar).
<!--more-->

Antes de nada quisiera agradecer la difusión que realizaron desde distintas administraciones públicas (el blog de la IDEE, el IECA o la IDERioja), asociaciones y grupos (Colegio Profesional de Geógrafos , Geoinquietos Valencia, Colegio Profesional de Geógrafos de Aragón o Asociación de ususrios QGIS de España), blog y páginas especializadas (NosoloSIG, Obermapa, Cartografía digital o Geotec UJI), y alguna que otra decena de profesionales (Sergio Domenech, David Piles, Gerson Beltrán, Carmen Diez, Paulino Vallejo, José María Martínez…) incluidos los propios ponentes.

Durante la preparación del encuentro, entre los varios correos mantenidos con los seis ponentes, se planteó la posibilidad de que tras la iniciativa se generara un **documento resumen de los puntos más relevantes que fueron tratados*. Aunque un poco extenso, fueron casi dos horas de evento, aquí lo tenéis. Si se quiere acceder a momento concreto de cada una de las intervenciones se ha añadido el enlace.

# Intervención de ponentes

Tras uno minutos introductorios, comenzamos el Geowebinar con una presentación a mi cargo ([3m:26s](https://youtu.be/7woNQVpS9V4?t=3m26s)). Se comentó el guión a seguir, cuál era el objetivo principal a tratar, una relación de temas principales y la presentación de los perfiles profesionales de los ponentes. 

<iframe src="//www.slideshare.net/slideshow/embed_code/key/s4HORJJBjua1mr" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> 

*[Presentación del Geowebinar. P. Soriano](http://www.slideshare.net/PatricioSoriano/presentacin-geowebinar-pautas-y-consideraciones-bsicas-para-la-entrega-de-proyectos-sig)*

El encargado de romper el hielo fue **José Luis Caballano** ([17m:38s](https://youtu.be/7woNQVpS9V4?t=17m38s)) de la Diputación de Córdoba. Inició su intervención con la definición de algunos conceptos y consideraciones básicas del **papel que juegan los datos espaciales y no espaciales dentro de la labor continua de toma de decisiones por parte de las administraciones públicas**. Se apuntó que la importancia de los datos geolocalizados es tal, que debería traducirse en la existencia de un departamento que vele por la creación del dato único y debería ser el receptor de los datos generados en proyectos. Esta “oficina SIG” deberá ejercer las función de proveedor de datos tanto a nivel interno, otros departamentos, como externo, empresas contratadas, otras administraciones….)

José Luis puso de manifiesto la necesidad de **generalizar los SIG como las herramientas más eficaces para tratar y producir datos geográficos frente a los sistemas CAD**. El uso de estos programas se completa con el manejo de bases de datos geográficas como formato de almacenamiento e intercambio. 

Una vez terminado el trabajo, **la entrega de la información producida y usada debería estar marcada por la posibilidad de su reutilización** posterior, pero definiendo unos protocolos de entrega lo suficientemente amplios para que puedan ser aplicados en otro tipo de proyectos. 

**Carlos López Quintanilla** ([26m38s](https://youtu.be/7woNQVpS9V4?t=26m38s)) de PGIS nos aportó el primer punto de vista como empresa. Carlos comentó que es fundamental que se se lleguen a **acuerdos entre empresa-administración en los que se pacte modelos de datos**. Estos modelos debe ser simples, fáciles de mantener y sencillos de completar. Así las empresas realizarán el encargo de forma ágil y puedan seguir con el el flujo de tareas y trabajos vinculados con el proyecto. A la vez, estos requisitos deberán contener como mínimo, una parte en común para que sirva para distintos ámbitos de trabajo (local, comarcal autonómico y nacional). La empresa podrían ampliar este modelo si lo viera oportuno para el proyecto, pero contaría con un documento de mínimos.

Según la experiencia de Carlos, es **muy recomendable el uso de formatos libres**. Esto evitaría problemas de compra de licencias, falta de soporte futuro y ahorro de costes. De forma específica se comenta que para proyectos de cierta envergadura puede usarse bases de datos geográficas como [Postgres/PostGIS](https://postgis.net/), mientras que para trabajos a escala más reducida es una buena opción las bases de datos en archivos como [SpatiaLite](https://en.wikipedia.org/wiki/SpatiaLite) o [Geopackage](https://www.geopackage.org/). **El uso de base de datos geográficas permite el diseño de modelos de datos más complejos**, la aplicación de restricciones, almacenado de simbología. Las posibilidades de estos formatos superan con creces el uso ficheros Shapefile. Para almacenamiento de datos ráster, las experiencias con el formato abierto [GeoTIFF](https://es.wikipedia.org/wiki/GeoTIFF) con la librería GDAL son positivas, sobre todo por la posibilidad de aplicarle parámetros de compresión, generación de estructurado de teselas.

Respecto a los metadatos de la información, se comenta que son fundamentales para que una vez pasado el tiempo, o cuando la información vuelvan a ser necesaria puedan ser “descubiertos” y comprendidos gracias a la información asociada y así permita su reutilización por cualquier persona o entidad que no sea su productor. **Junto a los metadatos es importante adjuntar la licencias de programas y datos, y si estas son [Creative Commons](https://es.wikipedia.org/wiki/Licencias_Creative_Commons) mucho mejor**.

El debate continuó ([34m:52s](https://youtu.be/7woNQVpS9V4?t=34m52s)) de la mano del arquitecto **José Carlos Rico** que presentó las **mecánicas de trabajo que están siguiendo para proyectos SIG** vinculados con el planeamiento y la planificación urbanística. De forma sencilla José Carlos describió la **estructura organizativa de los datos manejados para cada proyecto**, la definición de estilos asociados (por ejemplo qml de QGIS), la importancia de definir y "recortar" los datos base a partir de la definición del ámbito de trabajo, así como la opción de realizar entregables de un solo archivo de proyecto con todos los datos temáticos o varios por cada juego de resultados. Como tema recurrente se trata el tema de la información asociada al proyecto y a las capas, representada por la definición de unos metadatos mínimos, pensando en su reutilización futura.

A pesar de todo lo expuesto, y aunque esta situación va cambiando poco a poco, todo este esfuerzo y trabajo sistemático suele enfrentarse a la lamentable situación en la que **los principales interlocutores (administraciones públicas, otras empresas..) no solo no manejen SIG, si no que ni siquiera valoran sus posibilidades**. Una forma sencilla de plasmar esta situación es cuando se plantea la pregunta ¿me lo pasas a CAD? 

![Estructura organizativa de un Proyecto SIG. JC. RicoJC](/images/blog/201805_notas_geowebinar/estructura.PNG)

*Estructura organizativa de un Proyecto SIG. JC. Rico*

**Alejandro Alameda** ([41m:52s](https://youtu.be/7woNQVpS9V4?t=41m52s)) centró su presentación en aspectos vinculados la **generación y uso de los metadatos como elemento fundamental de un proyecto SIG** y por extensión de una IDE. Como punto de partida planteó que es necesario el conocimiento básico de la familia de las [normas ISO](http://metadatos.ign.es/normas-familia-iso19100) relacionadas con la generación de este tipo de información. **La creación de los metadatos será clave para posteriormente ser puedan ser usados en la definición de requisitos de un proyecto** en el que se vean involucrados esos datos. Este deberá ser nuestro foco principal en el uso de los metadatos.

Junto a otros apartados, título, productor, descripción, **la definición de los atributos de los datos es fundamental, ya que en ellos pueden encontrarse definidos los objetivos principales del encargo**. La falta de conocimiento de los datos a recoger, el escaso interés o pensar que es un trabajo demasiado tedioso son algunas de las causas por las se suele omitir su producción.

El conocimiento de estos metadatos, tanto por parte del cliente como de la empresa, servirá como documento que facilitará el entendimiento entre ambos. Estos ayudarán a **reducir las dudas posibles entre los objetivos reales del cliente y el trabajo que se haga**. Para ello puede usarse formularios o encuestas e incluirlos en un ciclo de validación, cuyo fin último sea la definición correcta de requisitos y necesidades.

Con respecto a las **medidas de calidad**, se indica que en general se suelen aplicar al revisar los datos por simple sentido común. El problema residen cuando estas medidas no se encuentran dentro de un protocolo e incluidas en el proceso de creación del dato, hecho que suele trasladar en la entrega de datos con errores. 

![Enlace a la presentación de A. Alameda](/images/blog/201805_notas_geowebinar/ppt_aalamenda.png)

*[Enlace a la presentación de A. Alameda](https://t.co/mIdcjttJlO)*

Una vez finalizado el trabajo y con las miras puesta en la entrega del mismo, se deberá generar los correspondientes **documentos descriptivos que acompañen a los datos, metadatos y memorias del proyecto**. Alejandro nos indicó también la importancia de añadir carpetas con los procesos, scripts, sentencias SQL, procesos en bach o herramientas de transformación de datos (ETL) usados. Será también recomendable indicar las incidencias encontradas. **Una buena documentación de nuestro proyecto/encargo ayudará facilitará la transferencia de conocimiento producido así como mejorará la reputación de la empresa responsable del encargo**. Para que esta acción sea rentable deberá encontrarse el término medio coste-beneficio. 

**David Portalés** ([57m11s](https://youtu.be/7woNQVpS9V4?t=57m11s)) nos aportó la perspectiva más informática del debate. Se trataron aspectos vinculados con los **entregables "informáticos" (código, plantillas, geoprocesos…)** y las opciones que desde su empresa ha ido encontrando con diferentes clientes. David comentó que es interesante la **entrega de fuentes y código generados**. Gracias a esto el código podrá ser reformado o reaprovechado posteriormente por el cliente. Por ejemplo, para trabajos para el sector público, junto a los soportes de entrega físicos habituales (DVD, memorias..) surge la opción de **subir al código a repositorios de versiones, tipo [GitHub](https://github.com/)**, lo que favorecerá sin duda los proyectos SIG. Se comentó el problema de las dependencias tecnológicas: librerías que hoy funciona pueden dejar de ser mantenidas o verse afectadas por modificaciones en su licencia. 

Cerrando el turno de palabra habló **Rafael Martínez** ([1h9m41s](https://youtu.be/7woNQVpS9V4?t=1h9m41s)) al que le tocó la no sencilla labor de realizar un resumen de los temas tratados y las aportaciones de cada uno de los ponentes. La síntesis se vio acompañada con aportes basados en su propia experiencia profesional. Rafa comienza indicando, que una de las causas que ha tenido la convocatoria, es por que en pocas ocasiones se han tratado de forma pública los problemas cotidianos que surgen entre el demandante del trabajo y el que lo tiene que hacer. 

Vuelve a comentarse el papel relevante que juega la Información Geográfica en los procedimientos administrativos, como comentó al inicio José Luis Caballano, superando la utilidad de los datos como mero apoyo cartográfico y remarcando su utilidad en la toma de decisiones sobre todo en proyectos de índole territorial. Rafael aumenta el alcance de la reutilización de la información que ha surgido en varias intervenciones. Para ello **se identifican las portales IDE y de Datos Abiertos como el espacio de difusión final de todos los datos que se producen en el proyecto**. Para que esto sea posible, nada mejor que asignarles una licencia abierta, siempre indicando el productor del dato. Esto es más que una opción es una obligación, al menos dentro de los datos y proyectos realizados con dinero público.

Como mejor método por superar las barreras impuestas la la denominada "filosofía CAD" se expone la **necesidad de mejorar la formación de empleados y técnicos sobre la importancia de los SIG y de los servicios vinculados con las IDEs**. No es cuestión de que deje de utilizarse estas potentes herramientas, sino de delimitar concretamente su aplicación, que no es la más idónea para proyectos geográficos.

Como es el caso de la mayoría de los ponentes y asistentes, al no venir del ámbito de la documentación, la cuestión de los metadatos se nos hace dura. Es sin embargo no es motivo para que no se genere. **Para facilitar de creación de los metadatos labor se propone el manejo de las normas técnicas ya existentes, como el perfil INSPIRE** y apoyarnos de los trabajos de investigadores en la materia como el profesor [F. Javier Ariza](http://orcid.org/0000-0002-5204-3630) de la Universidad de Jaén.

Para terminar, se comenta que sin duda **poder contar con profesionales y empresas informáticas especializadas en el campo geo será de gran utilidad** sobre todo a la hora de detectar y evitar errores en la calidad del dato. 

Terminado el turno de palabra se dedicaron los últimos minutos a contestar algunas **cuestiones planeadas en el chat** ([1h19m1s](https://youtu.be/7woNQVpS9V4?t=1h19m1s)).

**Carmen Diaz** realizó una consulta sobre la **formación sobre SIG** ¿es suficiente?¿en qué etapa formativa debería darse?¿solo en la universidad?¿podría incluirse la formación en esta materia en ciclos formativos vinculados como los de informática o delineación? Rafael Martínez, como representante del colectivo profesional, indica que debería ser en las asignaturas de Geografía donde tendría la mejor cabida estos aspectos de formación siempre usando los conocimientos apoyados por materias vinculadas con las tecnologías.

El **coste económico de la generación de los metadatos es tratado también por David Piles**. Este trabajo debe estar claro en lo presupuestos y no siempre las empresas están dispuestas a pagar por ellos.

Carlos López respondió una pregunta de **Gonzalo Pousa** sobre **tamaño de los archivos GeoTIFF**, indicando que el uso de la librería GDAL es básica para la compresión. Ese comentario se completa con el aporte de David Portáles sobre el equilibrio entre compresión y calidad. Para ellos se indica la bajada de precio sen los sistemas de almacenamiento que ayudan a no perder calidad.

En un momento del debate, Carlos nos da la importante noticia de la [creación de la Asociación de usuarios de QGIS España](http://www.qgis.es/), que favorecerá el conocimiento de esta potente herramienta SIG, que poco a poco va siendo implantada en las administraciones locales, como el Ayuntamiento de Barcelona.

Queda pendiente ver algunos aspectos fundamentales y a día de hoy totalmente factibles gracias a las herramientas que existen como es la **presentación de resultados mediante aplicaciones o servicios de mapas web**. Se hace referencia así a Carto, o a la iniciativa abierta de edición de información geográfica en Internet GeoWE.

# Algunas métricas y aportaciones técnicas

Creo que es también interesante indicar que, quitando algunas problemas técnicos sobre todo con el audio, el uso **YouTube Live** para la retransmisión del evento ha dado buenos resultados. El día del streaming hubo la posibilidad de coordinar la participación de seis ponentes, conectados desde varias partes de España, con dispositivos diferentes (pc, tablets, teléfonos), que compartieron presentaciones y sistemas operativos distintos. También indicar que la participación se abre gracias a la herramienta chat. Esto sin duda a requerido de unos ensayos previos e investigación sobre las posibilidades que ofrece la plataforma pero sin duda ha merecido la pena y permite tener un conocimiento acumulado para próximas experiencias.

Respecto a las *métricas*, de forma rápida indicar que hubo 115 accesos a la URL del evento, procedentes en un 75% de España. Durante la retransmisión hubo un pico máximo de 43 personas conectadas de las cuales unas 16 participaron en el chat. El vídeo tiene una duración total de 1:49 minutos y a fecha de esta publicación, 15 días después del evento, cuenta con 320 visualizaciones y 27 me gusta.

![Gráfico de visitas a la página del evento. Bitly](/images/blog/201805_notas_geowebinar/visitas2.png)

*Gráfico de visitas a la página del evento. Bitly*

# Como cierre...

Desde el punto de vista profesional, y porqué no personal, ha merecido la pena el esfuerzo y tiempo dedicado en la preparación del evento. Además de poder aportar a la comunidad sobre un tema candente, he tenido la oportunidad de establecer relación y “desvirtualizar” a otros profesionales del sector a los que sigo con interés hace tiempo. Gracias a sus aportaciones he podido aprender aún más en un tema de gran interés profesional y por lo que hemos tenido posibilidad de comprobar no del todo resuelto.

Se abre a partir de hora la lluvia de ideas sobre temas para futuros geowebinar...se admiten propuestas.

<iframe width="560" height="315" src="https://www.youtube.com/embed/7woNQVpS9V4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

*Vídeo completo*
