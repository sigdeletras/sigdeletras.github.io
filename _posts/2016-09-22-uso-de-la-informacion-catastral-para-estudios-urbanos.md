---
title:  "Uso de la información catastral para estudios urbanos"
header:
teaser: ""
categories: 
- blog
tags:
- catastro
- sig
- estudios urbanos
---

La cartografía catastral constituye uno de los conjuntos de datos de más uso en los Sistemas de Información Geográfica. A pesar de estar dentro de la categoría de cartografía temática ([Real Decreto 1545/2007](%20https:/www.boe.es/diario_boe/txt.php?id=BOE-A-2007-20556) ), su nivel de precisión (entre 1:500 y 1:5.000), la cobertura a escala nacional (salvo País Vasco y Navarra), la posibilidad de descarga mediante certificado, a través de la [Sede Electrónica de Catastro](http://www.sedecatastro.gob.es/) y las [características de la licencia de uso](http://www.catastro.meh.es/documentos/resoluciondgc20110323_tfs.pdf) , hace que muchos sistemas cartográficos, sobre todo de ámbito local, la estén utilizando como información topográfica de referencia.

De forma sencilla podemos definir la información catastral como aquella que recoge la descripción parcelaria o superficial de los bienes inmuebles. Para un descripción más detallada podemos usar la la siguiente  descripción de Sereno (2009) que se aplica al catastro en España:

_"Catastro Inmobiliario es un registro administrativo dependiente del Ministerio de Economía y Hacienda en el que se describen los bienes inmuebles rústicos, urbanos y de características especiales. La descripción catastral de los bienes inmuebles contenida en el Catastro Inmobiliario comprende sus características físicas, económicas y jurídicas, entre las que se encuentra la localización y la referencia catastral, la superficie, el uso o destino, la clase de cultivo o aprovecha- miento, la calidad de las construcciones, la representación gráfica, el valor catastral y el titular catastral."_  

Queda patente el gran interés que genera la información catastral, sobre todo para su reutilización en el sector productivo, generando nuevas oportunidades de negocio, con un coste muy bajo para el usuario y un alto grado de actualización y exhaustividad. El conocimiento de la estructura de datos catastrales debe generar nuevas vías de trabajo para las administraciones y en la investigación territorial y urbana.  Pero pese a las posibilidades y libertad de acceso, la información catastral tiene  poco uso más allá de ser usada como cartografía base. La principal razón de estos se debe a la dificultad técnica existente para explotar los datos, ya que requieren de ciertos conocimientos sobre la estructura de los datos catastrales y conocer qué información se puede extraer de ellos.

[![Superficie de la finca](https://c3.staticflickr.com/6/5284/29558797250_a061c8db66.jpg)](https://www.flickr.com/photos/115384326@N07/29558797250/in/dateposted-public/)

### Servicio de descarga

A través de la [Sede Electrónica de la Dirección General del Catastro](https://www.sedecatastro.gob.es/OVCFrames.aspx?TIPO=TIT), se puede hacer una descarga masiva de los datos catastrales no protegidos (todos salvo titularidad de inmuebles y valor catastral), tanto de la cartografía vectorial (en formato Shapefile) como de la información alfanumérica.  Para ello es necesario disponer de un certificado digital que permita autentificar frente a Catastro al usuario que solicita los datos. La información corresponde a municipios completos, en función de si es información de suelo urbano o rústico, con y sin historia. Estos datos se publican tres veces al año, a primeros de febrero, de junio y de octubre. Desde este [enlace](http://www.catastro.meh.es/ayuda/manual_descargas_shapefile.pdf) puede consultarse una guía de descarga redactada por la SEC.

La información cartográfica catastral se divide en urbana y rústica, para cada una de ellas se ha utilizado una escala de captura diferente. En el caso de la cartografía urbana la escala de captura está entre 1:500 y 1:1.000, y para la cartografía rústica entre 1:2.000 y 1:5.000.  Para la península y Baleares se utiliza un sistema de coordenadas proyectado, con el datum local ETRS89, y un sistema de representación cartográfico (o sistema de proyección) Universal Transversa Mercator (UTM), husos 29, 30 y 31\. Para Canarias se utiliza el datum global WGS84 y sistema de proyección UTM, husos 27 y 28.

El parcelario catastral se representa mediante cuatro geometrías principales MASA, PARCELA, SUBPARCE y CONSTRU. El resto de geometrías son auxiliares o contienen otros elementos cartográficos, como mobiliario urbano, límites administrativos, rótulos con los nombres de las calles, etc.

### Datos alfanuméricos catastrales

La cartografía catastral en formato SIG constituye la base a la que se asocia multitud de información alfanumérica descriptiva, tanto del suelo como de las construcciones. De esta forma, la plena identificación catastral se completa con la suma de información cartográfica e información alfanumérica.

[![Superfice contruida](https://c7.staticflickr.com/9/8324/29738357462_b5a5d141f2.jpg)](https://www.flickr.com/photos/115384326@N07/29738357462/in/dateposted-public/)

La descarga sigue los mismos mecanismos descritos obteniéndose la información en un fichero CAT.  El fichero .CAT está formado por texto plano tipo ASCII, donde cada registro (fila) tiene una longitud fija de 1.000 caracteres. Se descarga como un archivo comprimido en formato GZIP (extensión .gz). El archivo está formada por registros de varios tipos:

*   Tipo 01 y 90: Registro de cabecera y de cola. Los registros tipo 01 y 90 son accesorios ya que aportan datos sobre la fecha de los datos y el número de líneas que tiene cada registro tipo.
*   Tipo 11: Registro de Finca. Identifica y localiza a la parcela catastral.  De esta tabla podemos obtener principalmente datos de superficie: finca, construida, bajo rasante y cubierta  Existirá uno por cada parcela catastral implicada.
*   Tipo 13: Registro de Unidad Constructiva. Representa un edificio o un conjunto de construcciones particularizadas dentro de un edificio  Existirá uno por cada unidad constructiva en cada parcela catastral.
*   Tipo 14: Registro de Construcción. Identifica cada uno de los locales existentes en un bien inmueble, con su descripción física: superficie, antigüedad o tipología. Existirá uno por cada construcción de cada unidad constructiva en cada parcela catastral
*   Tipo 15: Registro de Inmueble. Identifica cada uno de los bienes inmuebles dentro de una parcela catastral. Existirá uno por cada bien inmueble en cada parcela catastral
*   Tipo 16: Registro de reparto de elementos comunes. Identifica el elemento constructivo cuyo valor se reparte entre los demás elementos de construcción. Existirá al menos uno por cada elemento común que se reparte, siempre que sea necesario especificar repartos especiales.
*   Tipo 17: Registro de cultivos. Identifica cada subparcela de cultivo existente dentro de la parcela catastral. Existirá uno por cada subparcela de cultivo existente dentro de la parcela catastral.

Los datos pueden ser transformados a formato tabular o importarlos a una base de datos en la que se replique la estructura de datos y se establezcan las correspondientes relaciones. Esto permitirá realizar operaciones estadísticas básicas como sumatorios, medias, máximas, mínimas o agrupaciones. Ya que nuestra finalidad es explotar los datos desde un punto de vista territorial es interesante añadir los datos alfanuméricos a una base con capacidades espaciales como puede ser PostgreSQL-Postgis.

### Usos

Actualmente, la información catastral constituye una información geográfica de referencia fundamental para una gran número de aplicaciones y sistemas de gestión de información geográfica temática, empezando por su aplicación más directa en la gestión de determinados impuestos, tanto estatales como autonómicos y locales, y siguiendo en aplicaciones más indirectas, como la gestión de usos y aplicaciones agrarias, el control y gestión de la ocupación del suelo, la gestión de la propiedad inmobiliaria, la gestión del patrimonio inmobiliario, la gestión del planeamiento o de obras, etc. (Sereno, 2009).

Tras el tratamiento correspondiente de los datos y su inclusión en un Sistema de Información Geográfica, podemos decir que contamos con un conjunto de datos de gran utilidad para estudios territoriales y urbanos.  Una primera explotación centrada en los datos geométricos nos podría dar **información de tipo físico**, dimensiones y formas las de parcelas o superficies de solar, sobre el parcelario catastral.

Al contar con la fecha de construcción/remodelación podemos obtener resultados que trabajen con la **variable temporal** analizando la antigüedad de edificios  que reflejan los momentos de comienzo y finalización en la construcción de los edificios que integran cada parcela.

[![Antiguedad](https://c3.staticflickr.com/6/5208/29558795610_fc2de0c68f.jpg)](https://www.flickr.com/photos/115384326@N07/29558795610/in/dateposted-public/)

Con la información que de los códigos de uso (UCM) se puede extraer, de manera selectiva para cada parcela,  los **usos del suelo**. A partir de estas capas pueden realizarse incluso trabajos de geomarketing vinculados por ejemplo a la identificación de usos prioritarios por vial o calle.

Para el  **planeamiento urbanístico**, los datos catastrales puede ser utilizados para el análisis de alturas máximas de edificación o la identificación de parcelas sobre sobreedificadas o subedificas a partir de la superficie y volumen construido. Igualmente podemos generar un mapa con el inventario del suelo disponible o de tipologías edificatorias/constructivas.

[![Número de usos por parcela](https://c1.staticflickr.com/9/8316/29738356552_18183fcfb7.jpg)](https://www.flickr.com/photos/115384326@N07/29738356552/in/dateposted-public/)

En el ámbito de la **Demografía**, si no disponemos acceso directo al padrón de habitantes, podemos seguir distintas metodologías para trasvasar de población desde las unidades censales a las parcelas catastrales. como la desarrollada por Santos Preciado (2015)  desarrolla esta metodología que permite el cálculo demográfico de forma proporcional según el peso del número de viviendas o de la superficie residencial construida en cada una de ellas.

Esta entrada es un ejemplo de los **servicios que desde SIGdeletras podemos ofrecer como consultaría especializada en Tecnologías de Información Geográfica con especial atención a trabajos para administraciones locales**. Para cualquier duda o consulta sobre éste o cualquier otro tipo de servicios se puede mandar un correo a la dirección **hola[arroba]sigdeletras.com.**

### Bibliografía utilizada

*   COCERO MATESANZ et al. (2014): La cartografía catastral y su utilización en los estudios urbanos, en un entorno SIG. Aplicación al análisis del municipio madrileño de Getafe. X_VI Congreso de Tecnologías de la Información Geográfica_. pp 648-662
*   CONEJO-FERNÁNDEZ, C. y VIRGÓS-SORIANO, L.I. (2001): SIGCA 2 Cartografía catastral digital, disponible para todos. _Catastro,_ 43, pp. 73-92.
*   DIRECCIÓN GENERAL DEL CATASTRO. (2011): _Fichero informático de remisión de catastro (bienes inmuebles urbanos, rústicos y de características especiales)._ 18 p. Obtenido de http://www.catastro.minhap.es/documentos/formatos_intercambio/catastro_fin_cat_2006.pdf
*   DIRECCIÓN GENERAL DEL CATASTRO. (2014): _Modelo de datos de cartografía vectorial (formato shapefile)._ 25 p. Obtenido de http://www.catastro.meh.es/ayuda/manual_descriptivo_shapefile.pdf
*   MORA-GARCÍA, R.T. et al. (2015): Reutilización de datos catastrales para estudios urbanos en DE LA RIVA, J., IBARRA, P., MONTORIO, R., RODRIGUES, M. (Eds.) 2015 A_nálisis espacial y representación geográfica: innovación y aplicación_. pp. 295-304
*   SANTOS PRECIADO, J.M. (2015): La cartografía catastral y su utilización en la desagregación de la población. Aplicación al análisis de la distribución espacial de la población en el municipio de Leganés (Madrid). _Estudios Geográficos. Vol. LXXV,I 278_, pp. 309-333
*   <span style="font-weight: normal;">SERENO ÁLVAREZ, A. (2009):</span> La información geográfica en España: especial referencia a la cartografía catastral. _Catastro_ 67, pp. 31-54.
