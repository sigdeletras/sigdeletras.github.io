---
title:  "SIG en la nube. Creando una capa a partir de un listado con coordenadas con GeoWE"
related: true
header:
  teaser: "/images/header/geowe.jpg"
categories:
- Blog
tags:
- GeoWE
- Sistemas de Información Geográfica
- Webmapping
---

Gracias a los comentarios y aportes de la comunidad  y el buen hacer de los desarrolladores del proyecto, **[GeoWE](http://geowe.org/)** va incorporando a sus funcionalidades herramientas que hace cada vez más sencillo realizar operaciones SIG en la nube. Aunque ya estaba disponible la carga de ficheros CSV con la información geográfica en formato WKT, en la versión Beta 1.3.8 se ha añadido la posibilidad de **cargar CSV pero con las coordenadas en columnas X e Y**. Esta mejora resuelve  un issue que puse en el [repositorio GitHub de GeoWE](https://github.com/geowe/geowe-core/issues/238). Es un buen ejemplo del flujo dinámico de trabajo que mantienen sus creadores.

Esta nueva mejora puede servir para cargar capas de puntos o vértices de trabajos topográficos. Puede  usarse igualmente para visualizar sobre una cartografía base los listados de coordenadas de ubicación o delimitación publicados en boletines o documentos oficiales.

### Un ejemplo: Localización de mojones de deslinde

El siguiente [enlace al Boletín Oficial del Estado](https://www.boe.es/diario_boe/txt.php?id=BOE-A-2016-5377) recoge una Orden por la que se aprueba el deslinde entre los términos municipales de Mendavia (Navarra) y Arrúbal (La Rioja). El documento añade al final una relación de coordenadas en el sistema geodésico de referencia ETRS89, proyección UTM huso 30, de las posiciones de los mojones del Acta.

Antes de poder ver cargar la información en GeoWE, el **primer paso es convertir este listado a formato CSV**. Hemos copiado la tabla a una hoja de cálculo, ordenandos las columnas para que los datos X e Y queden al final y reemplazando de forma masiva el símbolo decimal de coma a punto. Para terminar salvamos en formato CSV (deslinde.csv) delimitado por punto y coma. En los comentarios de issue podéis ver un ejemplo del modelo a seguir.

![Conversión de datos](/images/blog/12_geowe_csv/datos.png)

_Conversión de tabla en PDF a archivo CSV_

Para representar los datos, abrimos GeoWE y accedemos a _Menú>Capa>Añadir_. Una vez abierto el diálogo. pincharemos **en la pestaña "Archivo" cargaremos desde local el archivo CSV** (deslinde.csv). Antes de cargar, indicaremos el nombre de la capa, por ejemplo "Deslinde", el sistema de referencia EPGS:25830 (ETRS89 UTM30N) y el formato CSV. Tras hacer clic en "Aceptar", GeoWE nos presentará el resultado de la capa, representando de forma puntual cada coordenada de nuestro listado.

![Carga de archivo CSV](/images/blog/12_geowe_csv/geowe_puntos.png)

_Carga de archivo CSV en GeoWE_

### Creación de línea de deslinde con _snapping_

Gracias a las herramientas de GeoWE podemos algo más allá. Imaginemos que queremos crear una capa lineal a partir de los puntos cargados y que los vértices de la capa deben coincidir exactamente con los de a Orden.

En primer lugar, crearemos una capa vectorial vacía desde _Menú>Capa>Añadir._  Indicaremos el nombre de la nueva capa por ejemplo "Deslinde_lin" y el SRC. Generada la capa y para trabajar con precisión, activaremos la herramienta "_Snapping"_ que se encuentra el menú _"Capa"_. Para empezar a dibujar nuestro trazado, usaremos desde el menú _"Dibujo"_ la opción _"Línea"_ y acercaremos el curso a cada uno de los puntos hasta que veamos que se acerca automáticamente él e iremos dibujan la línea.

 ![Creación de capa lineal con snapping](/images/blog/12_geowe_csv/geowe_lin.png)

_Generación de capa lineal con la herramienta Snapping_

Generada la línea del límite, podemos salvar los resultados en distintos formatos geográficos estándares en nuestro ordenador en local o repositorio GitHub desde la herramienta de _”Exportar datos”_ del Administrador de capas.

### Análisis espacial. Parcelas afectadas

GeoWE añade en su versión Beta algunas operaciones de análisis. Entre ellas podemos encontrar la opción de **área de influencia o buffer**. Podríamos usar este geoproceso para identificar las parcelas catastrales afectadas por este nuevo deslinde. Si fuéramos los técnicos municipales de los ayuntamientos afectados usaríamos dicha referencia para comunicarla a los afectados, pasar la incidencia a Catastro y actualizar nuestro SIG Municipal.

Desde el menú _Capa>Análisis_ seleccionamos la opción _"Buffer"_, añadimos la distancia de 100 metros e indicamos que se calcule la influencia sobre la capa "Deslinde_lin"  

Si a**ñadimos el servicio WMS de  Catastro desde el catálogo de GeoWE**, podemos comprobar que las parcelas afectadas por el nuevo deslinde se sitúan al sureste. Para poder obtener la referencia catastral, marcaremos como activa la capa de catastro desde el _“Administrador de capas”_ y activaremos la herramienta _"WMS info"_ para obtenerla [información catastral](https://www1.sedecatastro.gob.es/CYCBienInmueble/OVCConCiud.aspx?del=26&mun=19&UrbRus=R&RefC=26019A001004280000DX&Apenom=&esBice=&RCBice1=&RCBice2=&DenoBice=.) pinchando dentro de la parcela.

C![Consulta de Parcela Catastral](/images/blog/12_geowe_csv/geowe_catastro.png)

_Consulta de información Catastral desde WMS_

### Pon un SIG Web en tu vida

Con una conexión de Internet, sin necesidad de instalar y configurar  en mi equipo ningún SIG, y a partir de un listado de coordenadas en PDF he podido realizar un trabajo técnico de una complejidad media. Poco a poco iremos viendo, que **a igual que otros flujos de trabajo se están ya realizando en la nube (ej. Google Drive), con herramientas como GeoWE este tipo de procedimientos SIG seguirán este mismo camino.**  

PD: ... que alguien le indique a Catastro que no ha actualizado en su servicio de mapas los nuevos límites municipales entre los términos Mendavia y Arrúbal ;-)
        
