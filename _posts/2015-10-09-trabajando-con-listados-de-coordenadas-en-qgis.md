---
title:  "Trabajando con listados de coordenadas en QGIS"
header:
      teaser: "/images/header/2015-10-09-cabecera_ategua.png"
categories: 
 - Blog
tags:
 - Formación
 - QGIS
 - Sistemas de Información Geográfica
 - Arqueología
---

En numerosas ocasiones el resultado de la toma de datos en campo con un GPS, una estación total o capturando datos sobre bases cartográficas es un listado de coordenadas que identifican una serie de localizaciones, como podrían ser elementos arqueológicos, un elemento poligonal como un entorno de protección o un corte, o una estructura lineal tipo infraestructura o camino.

<iframe style="border: 1px solid black;" src="/webpamming/visorategua/" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" width="100%" height="350"></iframe>

_Visor Zona Arqueológica de Ategua.BIC y entorno de protección. [Ver mapa más grande](/webpamming/visorategua/)_

Este tipo de información geográfica, me refiero al listado de coordenadas, suele ser solicitado por administraciones públicas como parte de los informes finales de proyectos y pueden encontrarse en boletines y publicaciones de la administración. Saber extraer esta información de nuestras entidades geográficas digitales o convertir estos datos en información que pueda ser tratada con una herramienta informática, como un SIG, puede ser un aprendizaje interesante y de gran utilidad desde el punto de vista profesional.

El [Sistema de Información Geográfica QGIS](http://www.qgis.org/es/site/), posee herramientas directas para convertir listados de coordenadas en formato tabla (CSV o TXT) en entidades geográficas puntuales. Si en las tablas existe otra columna que nos sirva para agrupar los datos,por ejemplo un código de yacimiento, estos datos pueden pasar a convertir de forma automática en líneas y estas a su vez en polígonos.

![ATEGUA. Banco imágenes IAPH. Autor: J.C. Cazalla](/images/blog/201510_visorategua/70_0006241.jpg "ATEGUA. Banco imágenes IAPH. Autor: J.C. Cazalla")

_Vista panorámica de Ategua. Fuente: Banco de imágenes IAPH. Autor: Cazalla, Juan Carlos_

Supongamos que tenemos un listado de coordenadas que identifican un bien arqueológico y también su entorno de protección. En este caso vamos a obtener los datos del [**yacimiento arqueológico de Ategua**](http://www.iaph.es/patrimonio-inmueble-andalucia/resumen.do?id=i2768) en la provincia de Córdoba. Los datos de las coordenadas del BIC y su entorno están disponibles en el Boletín Oficial de la Junta de Andalucía [(BOJA)  nº 244 de 16/12/2005](http://www.juntadeandalucia.es/boja/2005/244/35 "BOJA") . Lamentablemente  estos datos no están en el PDF en formato imagen por lo que tendremos que ir copiando manualmente las coordenadas en una hoja de cálculo en la que se incluya  el número de orden la coordenada, el valor de X y el valor de Y. Como tenemos la información tanto del BIC como del entorno , vamos a añadir una nueva columna al principio que denominaremos entidad, donde quedará reflejado si la coordenadas es de la Zona Arqueológica o del Entorno.

Una vez obtenidos los datos, pasaremos la tabla a formato CSV, utilizando las opción de Guardar como de nuestro programa de hoja de cálculo, en mi caso Calc de LibreOffice. El formato csv no es más que un texto plano donde cada fila es un registro de la tabla, y en que los valores por columnas se encuentra separado por comas. Es un formato estándar que suele poder cargarse en la mayoría de los programas que trabajan con datos tabulares como las bases de datos o las hojas de cálculo, o en nuestro caso los SIG.

![](/images/blog/201510_visorategua/datos.png)

_Listado de coordenadas en hoja de cálculo y archivo CSV._

Una vez que tengamos nuestro csv, abrimos QGIS y seleccionamos el Sistema de Coordenadas de Referencia en el que se encuentren los vértices. Aunque en el BOJA, no se hace referencia al SRC, aunque debería, por la fecha estos datos están en ED50 UTM30N.

Para añadir la tabla de coordenadas, usamos la opción **“Añadir capa de texto delimitado”** del menú Añadir Capa. Indicaremos la ubicación del archivo CSV, indicaremos el tipo y comprobaremos que QGIS a seleccionado las columnas correctas para las coordenadas X e Y. Una vez revisado las opciones, pulsamos en aceptar y tendremos representados las coordenadas de  nuestra tabla en puntos. La capa se genera de forma temporal por lo que si queremos trabajar con ella podemos guardarla en Shape o almacenarla en nuestra base de datos PostGIS o SpatiaLite. Para una mejor compresión de los datos podemos cargar cartografía base o alguna ortofoto como las del PNOA.

![](/images/blog/201510_visorategua/carga_csv.png)

Para pasar los datos puntuales a lineales o poligonales y mejorar la compresión de la información, vamos a utilizar dos procesos de la caja de Herramientas.

*   **_Point to path_** nos generará una línea según el orden de los puntos (Campo de Orden) y utilizará los datos de la columna entidad para agrupar los trazados (Campo de Grupo).
*   Con **_Lines to Polygon_** generaremos una nueva capa poligonal a partir de las líneas. Tendremos que tener en cuenta que nos generará un polígono para la delimitación de la Zona Arqueológica y otro para el Entorno de Protección  por lo que una vez ejecutado será interesado obtener dos capas poligonales con cada una de las entidades.

![](/images/blog/201510_visorategua/proceso.jpg)

Este manual forma parte del temario del [**curso  _on line_ “Sistemas de Información Geográfica y Arqueología”**](http://www.almagre.es/cursos-formacion/curso-online-sistemas-de-informacion-geografica-qgis-y-arqueologia "Curso Almagre") organizado por Almagre. Para más información puede consultarse la página del curso en la web del curso.
        