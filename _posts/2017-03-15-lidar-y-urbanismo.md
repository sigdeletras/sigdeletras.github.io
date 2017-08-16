---
title:  "Lidar y Urbanismo"
header:
  teaser: "/images/header/img_cabcera_plugin.jpg"
categories: 
  - blog
tags:
  - LiDAR
  - Urbanismo
  - QGIS
  - Sistemas de Información Geográfica
  - Lastools
---

Desde hace unos años, los datos [LiDAR](https://wikipedia.org/wiki/LIDAR "Lidar Wikipedia") se han convertido en la fuente de datos geográficos “de moda”. LiDAR un sistema de medida basado en determinar la distancia desde un emisor láser a un objeto, midiendo el tiempo transcurrido entre la emisión del pulso láser y la recepción de la señal reflejada por el objeto.

La información que capturan (coordenadas, altura, retorno, ángulo de barrido) y la precisión (puntos por metros cuadrados) han permitido una magnífica incorporación en trabajos vinculados con estudios de biomasa, inundaciones, mapas de ruido, explotación de minas, [arqueología](2016/trabajando-con-datos-lidar-algunos-ejemplos-del-conjunto-arqueologico-de-madinat-al-zahra "Lidar y Arqueología en SIGdeletras") o simplemente en trabajos topográficos y cartográficos de detalle entre otros.

![Lidar imaging comparing old-growth forest (right) to a new plantation of trees (left).](/images/blog/201703_lidar_urbanismo/Forest_LIDAR.jpg "Lidar e Ingeniería Forestal (Wikipedia https://en.wikipedia.org/wiki/Lidar)")

_Lidar imaging comparing old-growth forest (right) to a new plantation of trees (left).[Wikipedia](https://en.wikipedia.org/wiki/Lidar)_

Tras la captura de datos, la clasificación, automática y manual, de la nube de puntos (ecos o retornos) es un proceso fundamental para poder sacarle el máximo rendimiento a esta fuente de información. En esta clasificación, los pulsos con un único retorno suelen ser interpretados como superficies sólidas o duras (edificios, suelo, etc.), en el agua el rayo láser es absorbido rápidamente y no vuelve al avión (no retorno) y la vegetación podemos tener varios retornos ya que el rayo recorre desde la copa hasta el suelo.

### LiDAR y Urbanismo

En el ámbito de los estudios urbanos esta técnica se presenta muy prometedora, ya que en una primera aproximación, posibilitan un **levantamiento rápido y preciso de una zona amplia, con un error del orden de centímetros**, reduciendo también de manera drástica el tiempo necesario para la toma de datos.

Los datos están siendo usados en la **actualización catastral** ya que permiten por ejemplo la detección de nuevas edificaciones gracias el registro de cambios volumétricos o la construcción de piscinas. Los **modelos 3D** de áreas urbanas generados a partir de fuentes LiDAR pueden ser utilizados para estudios de densidad de edificios o determinación de número alturas de edificación.

En el **curso titulado [SIG y Ciudad](2017/curso-semi-presencial-sistemas-de-informacion-geografica-aplicados-al-analisis-urbano-y-del-territorio "Curso SIG y Ciudad")** que imparto con el arquitecto [José Carlos Rico](https://twitter.com/jcricocordoba?lang=es "Twitter José Carlos Rico") hemos querido incorporar esta fuente de datos a los flujos de trabajo de los profesionales vinculados con el urbanismo.

Trabajando con los datos del [LiDAR PNOA](http://pnoa.ign.es/presentacion "Lidar PNOA"), cuya densidad es de 0,5 puntos/m² y con una precisión altimétrica de 20 cm RMSE Z y tras la generación de Modelos Digitales del Terreno, estos modelos pueden usarse por ejemplo para :

*   Obtención de cotas máximas, mínimas y rangos de las distintas zonas de una figura de planeamiento.
*   Generación de curvas de nivel con equidistancias de 1 a 0,5 metros para planos topográficos o de replanteo.
*   Creación de perfiles de alturas de la red de infraestructuras viarias proyectadas.
*   Extracción de altura de construcciones existentes

### Herramientas

Una vez obtenidos las cuadrículas LiDAR de la zona de trabajo se puede utilizar la herramienta [Lastools](https://rapidlasso.com/lastools/ "Lastools") para realizar unión de ficheros (lasmerge) o recortes (lasclip) mediante polígono. A partir de estos primeros trabajos pueden generarse distintos modelos digitales de elevación de gran resolución. Jugando con la clasificación de la nube de puntos podemos obtener **modelos de terreno (MDT)**, forma tridimensional del terreno desnudo en el que se excluye cualquier elemento situado sobre él, o **modelos digitales de superficies (MDS)** que incluyen el terreno y los elementos estáticos situados sobre ella (árboles, edificios, etc).

![Modelos Digitales de Elevación a partir de los datos LiDAR PNOA](/images/blog/201703_lidar_urbanismo/pnoa_mds_mdt.png "Modelos Digitales de Elevación a partir de los datos LiDAR PNOA")

_PNOA y Modelos Digitales de Elevación (MDS y MDT) partir de los datos LiDAR PNOA_

Con nuestro modelo digital del terreno, podemos trabajar con las distintas herramientas y geoprocesos para datos ráster que nos ofrece el potente SIG de escritorio [QGIS](http://www.qgis.org/es/site/%20 "QGIS").

#### **Modelos digitales del terreno**

Desde el modelo de elevaciones pueden crearse mapas de pendientes, orientaciones, escabrosidad. La calculadora ráster es la herramienta que nos permitirá filtrar las capas capas para que cumplan determinados criterios. Así podemos seleccionar zonas que cumplan una serie de criterios topográficos (ej. orientación al sur y pendiente menor de cinco grados) favorables para su edificación.

![Mapa de pendientes (%)](/images/blog/201703_lidar_urbanismo/pendiente.png "Mapa de pendientes (%)")

_Mapa de pendientes (%)_

#### **Curvas de nivel**

La resolución de los datos de partida nos permite generar curvas de nivel cada metro o medio metro. Esto nos permitiría contar con un plano topográfico de detalle sobre el que trabajar. Aplicando determinadas reglas en la simbología y etiquetado de la capa de curvas se pueden obtener resultados profesionales.

#### **Estadística zonal**

Mediante esta herramienta de QGIS se podrán obtener un conjunto de estadísticas bastante amplias sobre los valores del modelo de elevaciones para las geometrías de una capa poligonal. Se puede usar la estadística zonal para obtener las cota máxima, mínima y la diferencia entre ambas de las determinadas manzanas o o parcelas proyectadas en una figura de planeamiento. Esta información será de utilidad por ejemplo para cálculos de volumetrías.

![Plano temático por intervalo entre cota máxima y mínima de capa manzana de planeamiento](/images/blog/201703_lidar_urbanismo/tematico_intervalos_cotas.png)

_Plano temático por intervalo entre cota máxima y mínima de capa manzana de planeamiento_
