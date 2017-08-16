---
title:  "Primeros pasos CARTO Builder. Mapa de edificios de Sevilla"
header:
  teaser: ""
categories:
  - blog
tags:
  - Carto
  - Catastro
  - Sevilla
  - Ciudad
---
        
Hace tiempo que tenía pendiente probar **Builder,** la nueva herramienta de [CARTO.](https://carto.com/ "Carto Web") Junto a una gran cantidad de cambios en la interfaz y en el flujo de trabajo, a los que habrá que ir poco a poco acostumbrándose, existen dos novedades que hacen de Carto la empresa más potente a día de hoy  que aplicada el modelo _SaaS_ al ámbito de los ‘mapas’. La primera novedad es la  la incorporación de asistentes para la realización de análisis espaciales y la segunda la posibilidad de añadir a nuestros mapas  aplicaciones o complementos (_widgets_) basados en los datos disponibles.

En el antiguo [_Editor_](https://carto.com/docs/carto-editor/ "Carto Editor") podrían realizar mediante consultas SQL y funciones espaciales gran cantidad de análisis derivados de nuestros datos geográficos. Toda esta potencialidad es ahora bastante más accesible con [**Builder**](https://carto.com/builder/ "Carto Builder"). Gracias a un conjunto de asistentes gráficos, el usuario puede crear de forma rápida complejos procesos espaciales como identificar lugar central, generación de líneas a partir de puntos, áreas de influencia, filtrado, análisis cluster... Para más información sobre estos procesos puede consultarse las [guías en la web](https://carto.com/learn/guides "Carto Guides") de CARTO.

![Asistentes análisis Carto](/images/blog/12_builder/analisis.png "Asistentes análisis Carto")

_Asistentes de análisis CARTO_

Con la incorporación de  _widget_  a nuestro mapa, podemos añadir valor a la representación gráfica de la información.  La visualización de datos estadísticos  o gráficos mejora  la compresión de los mapas y pueden ayudar a identificar nuevos puntos de vista. Estos complementos  permiten por ejemplo, añadir datos estadísticos como totales, valores medios, máximos o porcentajes. También  pueden usarse para presentar agrupaciones  o categorías de datos por campos y mostrarlos  infografías interactivas o histogramas de series temporales.

![](/images/blog/12_builder/widgets.png)

_Ejemplos de widgets_

### Edificios de Sevilla

Como ejemplo del potencial del nuevo _dashboard_ he realizado un [**mapa de los Edificios de la ciudad de Sevilla (España)**](https://sigdeletras.carto.com/builder/55db719a-bdf4-11e6-ae20-0e05a8b3e3d7/embed "Mapa Edificios de Sevilla"). Estos datos proceden de los [servicios Inspire de Cartografía Catastral](%20http:/www.catastro.minhap.gob.es/webinspire/index.html "Catasttro Inspire") de la Dirección General de Catastro. En concreto de la capa edificios (_BU buildings_)

![Visor Carto de Edificios de Sevilla](/images/blog/12_builder/mapa.png "Visor Carto de Edificios de Sevilla")

_Click_ en la imagen para acceder al mapa ["Edificios de Sevilla"](https://sigdeletras.carto.com/builder/55db719a-bdf4-11e6-ae20-0e05a8b3e3d7/embed "Carto Mapa Edificios de Sevilla")

La representación y datos sobre los edificios es gran **utilidad en el ámbito de lo público** ya que permite conocer los parámetros urbanísticos de las ciudades, realizar investigaciones sobre crecimiento o estudios prospectivos. De igual manera, el conocimiento del parque edificado es fundamental para trabajos de sostenibilidad urbana vinculados con la ocupación del suelo o los usos e intensidades edificatorias. En el **sector privado** estos datos están siendo explotados desde el punto de vista  inmobiliario y en geomarketing. Para más información sobre las posibilidades de la información Catastral pueden consultarse esta [entrada en el blog](http://sigdeletras.com/2016/uso-de-la-informacion-catastral-para-estudios-urbanos "Uso de la información catastral para estudios urbanos ").

Antes de subir el conjunto de datos a CARTO, el gran volumen de información descargada fue almacenada en una base de datos geográfica PostgreSQL-Postgis. La causa de este trabajo previo se ha ha debido a dos razones. En primer lugar, debemos de tener en cuenta el tipo [cuenta o plan](https://carto.com/pricing/ "Carto accounts") que disponemos en CARTO, que entre otras cuestiones definirá  el volumen de megas disponibles. La segunda razón es la de poder disponer en local (SIG) de nuestros datos. Gracias a esto podremos realizar determinadas operaciones SIG de filtrado, transformación y enriquecimiento con otros recursos antes de subir los datos a la web. Por ejemplo, para este ejemplo han sido seleccionados solo algunos atributos de la capa de edificios  y se le ha añadido mediante una vista la [delimitación de los barrios de Sevilla](http://www.juntadeandalucia.es/institutodeestadisticaycartografia./DERA/index.htm "Barrios DERA IECA") ofrecida por el IECA.

Tras subir nuestros datos en CARTO, contamos en primer lugar con un mapa con la representación de los datos geográficos de los edificios del municipio de Sevilla. Para cada edificio puede consultarse la información suministrada por Catastro (referencia, imagen, uso dominante, área, número de viviendas…) y datos del distrito y barrio. Podemos personalizar la ventana de datos con un poco de código HTML que permita  por ejemplo para añadir un enlace a Catastro o la imagen de fachada.

![Ventana de datos asociados al Edificio](/images/blog/12_builder/ventana.png)

_Ventana HTML de datos asociados al Edificio_

Utilizando los widgets de CARTO Builder he añadido la siguiente información complementaria:

*   **Nº de edificios:** Calcula el total de edificios representados en del mapa. Al hacer zum se recalcula el total según el área de visualización.
*   **Edificios por barrio:** Permite filtrar el conjunto de edificios por barrios.
*   **Uso dominante:** La capa catastral adjunta el uso dominante del edificio incluyendo las categorías Vivienda, Industrial, Comercial, Agricultura, Oficinas y Edificios públicos.  El valor se obtiene calculando el uso  que mayor superficie tenga de todos los inmuebles de la parcela catastral donde esté el edificio.
*   **Fecha de construcción:** En el modelo de Inspire esta fecha se define por los atributos _beginning y end_. Para nuestra aplicación ha sido cargada exclusivamente la más antigua y presentada en un histograma.  Este _widget_ es también dinámico ya que se puede acotar la serie temporal mediante fechas de inicio y final.

![Filtro de edificios de uso dominate de tipo comercial del barrio de El Arenal (Sevilla)](/images/blog/12_builder/uso_comercial_arenal.png "Filtro de edificios de uso dominate de tipo comercial del barrio de El Arenal (Sevilla)")

_Filtro de edificios de uso dominante de tipo comercial del barrio de El Arenal (Sevilla)_

### Conclusiones

Con la nueva plataforma de Carto queda reflejada a la perfección el [nuevo rumbo que ha tomado la empresa](http://www.abc.es/tecnologia/informatica/software/abci-nuevo-golpe-cartodb-pasa-carto-y-apuesta-retorcer-mapas-interactivos-201607071529_noticia.html "Noticia ABC"). Los nuevos desarrollos están enfocados en permitir al usuario ahondar más en la información y datos presentados en los mapas y que a partir de estos  pueda realizar nuevas preguntas, obtener  conclusiones y tomar decisiones.

Si estáis interesados sobre el desarrollo de este trabajo o ver las posibilidades en vuestras entidades no dudéis en contactar conmigo a través del correo **hola[arroba]sigdeletras.com**.
        
