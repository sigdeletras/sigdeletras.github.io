---
title:  "Convertir archivos CAD de ED50 a ETRS89 con la aplicación Calar."
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201710_calar/calar.PNG"
categories: 
  - 2017
tags:
  - CAD
---

Cecilia antigua alumna arquitecta del curso  “SIG y Ciudad. Sistemas de Información Geográfica aplicados al análisis urbano y del territorio” nos consultó hace unos días la mejor forma de transformar  el sistema de coordendas de ED50 a ETRS89 de un archivo CAD.

<!--more-->

Durante el curso, vimos como desde QGIS se podía diseñar una sistema personalizado de coordendas para proyectar al vuelo capas en ED50 a ETRS89. Para ello era ncesario utilizar la rejilla de transformación del IGN. También hicimos alguna práctica para transformar definitivamente capas al sistema geodésico de referencia oficial de España.

A pesar de la potencia del SIG en esta materia, la cosulta se centraba directamente en la transformación desde aplicaciones CAD. Muchos profesionales y estudios de arquitectura están realizando textos refundidos del planeamiento municipal y parten de trabajos hechos en ED50. Sin embargo se les solicita que las planimetrías finales se encuentren en ETRS89.

Si no se dispone de un software tipo AutoCAD Map 3D, se puede usar algunas de las aplicaciones de transformación de coordenadas existentes. Muchas de ellas son de libre acceso ya que están desarrolladas por los mismos organismos productores de información geográfica. En este caso pensamos que la **calculadora geodésica Calar**, herramienta incluída en el SIG corporativo de la Junta de Andalucía, puede ser de utilidad para este tipo de trabajos.

## De DWG a DXF.

Lamentablememente la aplicación no trabaja con archvivos propietarios dwg. Previamente debemos usar algún programa CAD para convertir los archivos a DXF, y si es a DXF versión 2010, mejor que mejor. 

## Calar. Descarga e instalación.

[Calar](http://www.juntadeandalucia.es/organismos/empleoempresaycomercio/areas/estadistica/cartografia/paginas/cliente-geodesia.html) es tanto un [calculadora geodésica online](http://www.juntadeandalucia.es/servicios/mapas/geodesiaclient/), como una aplicación de escritorio diseñada para facilitar la transformación de la información espacial contenida en los ficheros SIG en los formatos más comunes  (DXF, DGN, Shape...) entre los diversos sistemas de referencia oficiales en Andalucía y España.

![Calar. Calculadora geodésica online](/images/blog/201710_calar/servicio.PNG)

Para este caso vamos a utilizar la aplicación, ya que nos permite transformar ficheros CAD. La descarga de Calar se encuentra disponible en la página web del [repositorio de software libre de la Junta de Andalucía dentro del proyecto SIG Corporativo](http://www.juntadeandalucia.es/repositorio/usuario/peticiones/directaInfoBasica.jsf?linkDummyForm:_idcl=items_descarga:15:items_descarga:0:_id191&).

![Repositorio de software libre de la Junta de Andalucía dentro del proyecto SIG Corporativo](/images/blog/201710_calar/repositorio.PNG)

## Configuración de la rejilla de cambio de datum

Calar utiliza un fichero de rejilla de mínima distorsión en formato NTv2 para calcular las conversiones de coordenadas entre los distintos datums soportados. 

Ya que la aplicación tiene un tiempo, es interesante descarga el [fichero que proporciona el Centro Nacional de Información Geográfica](http://www.ign.es/web/ign/portal/gds-rejilla-cambio-datum) y configurar la aplicación para utilizar este fichero. 

![Descarga rejilla NTv2 IGN](/images/blog/201710_calar/rejilla.PNG)

Para ello hay que ir a la carpeta en la que se haya instalado la aplicación Calar y abrir el archivo *res/data/config.ini* con cualquier editor de textos.  Por ejemplo en Windows el archivo está en *C:\Program Files (x86)\Calar\res\data*

Podemos copiar el archivo de la rejilla (PENR2009.gsb) en la misma carpeta y editar el archivo *config.ini* cambiando el nombre del fichero.

	ed_etrs_grid = res/data/PENR2009.gsb.gsb

## Transformando un archivo DXF CAD

Una vez instalado y configurado Calar, abrimos el programa. 

- Elejimos los Sistema de referencia de origen (ED50) y destiano (ETRS89). En este caso trabajaremos en proyección UTM 30N.
- Selecionamos la pestaña **Fichero** e indicamos el archivos dxf de salida y la ruta y el nombre del archivo de salida ya transformado.
- Para finalizar hacemos clic en **Transformar**

![Calar. Ficheo DXF](/images/blog/201710_calar/dxf.PNG)

Existe la posibilidad de realziar esta misma operación por lotes, es decir realizando la transformación de varios ficheros a la vez. 

## 2015 fecha topoe según el RC 1071/2007.

En el REAL DECRETO 1071/2007, de 27 de julio, por el que se regula el sistema geodésico de referencia oficial en España, se adopta el sistema ETRS89 (European Terrestrial Reference System 1989) como nuevo sistema de referencia geodésico oficial en España. En este mismo decreto se dispuso un periodo transitorio hasta el 2015 en el que podrán convivir ambos sistemas. Esto significa que a fecha de hoy, todos los organismos oficiales productores de cartografía debería utilizar y ofrecer sus productos cartográficos en ETRS89. 

Sin duda, herramientas como Calar sonde gran utilidad para un número pequeño de ficheros. Pero si tenemos la necesidad **transformar grandes cantidades de ficheros puede que sea de interés contar con servicios profresionales que garanticen este trabajo**. Sobre este tema, y para cualquier consulta no dudéis en consultar con nosostros.