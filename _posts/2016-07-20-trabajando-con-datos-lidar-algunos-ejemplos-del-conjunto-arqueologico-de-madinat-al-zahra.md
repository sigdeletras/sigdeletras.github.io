---
title:  "Trabajando con datos LiDAR. Algunos ejemplos del Conjunto Arqueológico de Madinat al-Zahra"
excerpt_separator: "<!--more-->"
comments: true
header:
  teaser: "/images/header/2016-07-20-lidar_sombras.png"
related: true
categories: 
  - 2016
tags:
  - LiDAR
  - Arqueología
  - Patrimonio
  - LAStools
---

El LiDAR (de light detection and ranging) es una técnica de teledetección óptica que utiliza la luz de láser para obtener una muestra densa de la superficie de la tierra produciendo mediciones exactas de x, y y z. LiDAR, que se utiliza principalmente en aplicaciones de representación cartográfica láser aéreas, está surgiendo como una alternativa rentable para las técnicas de topografía tradicionales como una fotogrametría. Cada punto LiDAR que es postprocesado puede tener una clasificación que define el tipo de objeto que reflejó el pulso láser. Los puntos LiDAR se pueden clasificar en varias categorías que incluyen suelo o terreno desnudo, parte superior de cubierta forestal y agua. (Fuente: [http://desktop.arcgis.com/](http://desktop.arcgis.com/es/arcmap/10.3/manage-data/las-dataset/what-is-lidar-data-.htm))

<!--more-->

Esta fuente de datos tienen múltiples aplicaciones: modelos digitales del terreno y de superficies (con edificios y vegetación), estudios de zonas inundables, detección automática de edificaciones nuevas, estudios de visibilidad y cobertura de antenas, inventarios forestales (cobertura arbórea y de matorral, las alturas máximas de la vegetación, la presencia de matorral o regeneración avanzada), etc.

Gracias al [Plan Nacional de Ortografía Aérea](http://pnoa.ign.es/presentacion) contamos con cobertura de datos LiDAR para España (distintas fechas según Comunidades Autónomas). Los datos LiDAR del PNOA tienen una una densidad de 0,5 puntos/m y una precisión altimétrica obtenida es mejor de 20 cm RMSE Z. Los datos se distribuyen a través del [Centro de Descarga del CNIG](http://centrodedescargas.cnig.es/CentroDescargas/buscadorCatalogo.do?codFamilia=LIDAR) en ficheros digitales de 2x2 km de extensión. El formato de descarga es LAZ (formato de compresión de ficheros LAS).

![](/images/blog/cnig.png)

### LiDAR en Arqueología

Los datos LiDAR están siendo usados de profusamente utilizados en el campo de la Arqueología. La densidad de la cobertura y la posibilidad de poder obtener modelos digitales del terreno de detalle están dando magníficos resultados sobre todo en la detección de estructuras de gran tamaño (murallas, zanjas, construcciones) en zonas de densa vegetación. Los ejemplos son numerosos, pero pueden ilustrar bien este texto los trabajos del grupo de investigación [Roman Army](http://romanarmy.eu/es/)  sobre arqueología militar romana en el norte de España o el proyecto [Cambodian Archaeological Lidar Initiative (CALI)](http://angkorlidar.org/) que investiga la red de ciudades medievales del imperio Jemer sepultadas bajo la jungla en Camboya.

![](/images/blog/lidar_romana.png)

_Imagen: João Fonte e Luis Gonçalves 2016\. [O uso combinado de LiDAR, QGIS e LAStools aplicado ao estudo de paisagens arqueológicas](http://qgis.pt/apresentacoes_qgis2016/QGISPT-Fonte-Seco.pdf)._

### Algunos ejemplos para el Conjunto Arqueológico de Madinat al-Zahra

Mi interés por los datos LiDAR se centran, a día de hoy, más en las posibilidades que ofrece en ámbitos urbanos y su estudio desde el punto de vista geográfico. Este interés no ha impedido que,tras la reciente apertura de los datos LiDAR para Andalucía, haya realizado algunas pruebas con distintos software ([LAStools](https://rapidlasso.com/) de Martin Isenburg y [FrugoViewer](http://www.fugroviewer.com/)) específicos y también con QGIS sobre algunos yacimientos emblemáticos de la provincia de Córdoba (Ategua, Torreparedones, Madinat al-Zahra, etc).

![](/images/blog/07_medina_lidar/pnoa.png)

_Localización del Conjunto Arqueológico de Madinat al-Zahra (Córdoba) sobre WMS ortofotografíal del PNOA © Instituto Geográfico Nacional de España)_

La imagen de más impacto es la obtenida para el ámbito de la [ciudad palatina de Madinat al-Zahra](https://es.wikipedia.org/wiki/Medina_Azahara). Los resultados no son nada novedosos ya que en la documentación planimétrica del Plan Especial de Protección del Conjunto ya existía un plano estructuras no excavadas  seguramente obtenidos a partir de algún tipo de prospección geofísica.

 ![](/images/blog/07_medina_lidar/pepma.png)

_B2 - Estructura urbana de Madinat al-Zahra. Interpretación de los restos no excavados. PEPMA (Fuente: [GMU Córdoba](http://www.gmucordoba.es/planes-especiales))_

Junto a los restos visibles en la actualidad el mapa de sombras generado a partir de la nube de puntos filtrados (sólo terreno) es bastante espectacular, pudiéndose nuevas estructuras no documentas en el plano del PEPMA.

 ![](/images/blog/07_medina_lidar/lidar_sombras.png)

Generación del mapa de sombras con los datos filtrados no es definitiva. Podemos ir modificando los pámetros de altitud/azimut de la luz y factor del valor Z (exageración vertical)  para obtener nuevos conjuntos de datos.

 ![](/images/blog/07_medina_lidar/parametros.png)
        
