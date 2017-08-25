---
title:  "Creación de máscara de visualización con estilo de polígonos invertidos con QGIS"
excerpt_separator: "<!--more-->"
comments: true
related: true
categories: 
      - 2014
tags:
      - QGIS
      - Sistemas de Información Geográfica
      - Carto
---

Lo había visto publicado dentro del listado de novedades de la última versión de QGIS, pero aún no había legado el momento de utilizarlo. Desde la versión 2.4 Chugiak de QGIS se puede utilizar un determinado polígono para crea una máscara opaca que oculte los datos fuera de ese polígono y muestre sólo la información incluida dentro del mismo.

Por ejemplo, preparando un proyecto del Distrito Municipal de Verón Punta Cana de la República Dominicana, necesito visualizar sólo los datos incluidos dentro de la sección censal de "El Salado", de tal forma que se vean sólo los ámbitos de barrios dentro de esta sección y de fondo la información de Google Maps.

[![01_mascara_vista_principal]()]

_Información Geográfica DM Verón-Punta Cana. Fuente ONE_

El primer paso tras cargar las capas vectoriales y definir su estilo de visualización almacenado en una [base de datos Spatialite](http://sigdeletras.com/2014/articles/trabajando-con-spatialite/) y añadir con el plugins Openlayer la capa de GoogleMaps, es realizar un filtrado de datos mediante el Constructor de consultas disponible en formulario Propiedades. De esta forma obtendremos un subconjunto de datos que utilizaremos para realizar la mascara.

[![02_mascara__constructor de consultas_qgis](https://camo.githubusercontent.com/f41792781156ccdc552b754a8bea1a4f1c3e6cc9/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353535372f31343835353534363138395f323331343863336136305f7a2e6a7067)](https://camo.githubusercontent.com/f41792781156ccdc552b754a8bea1a4f1c3e6cc9/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353535372f31343835353534363138395f323331343863336136305f7a2e6a7067)

_Creación de consulta_

[![02_mascara_el_salado](https://camo.githubusercontent.com/e250230935532d469bc29cd6df72e688e9bbe07c/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353537382f31343835353731343938375f646662336664383534625f7a2e6a7067)](https://camo.githubusercontent.com/e250230935532d469bc29cd6df72e688e9bbe07c/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353537382f31343835353731343938375f646662336664383534625f7a2e6a7067)

_Resultado de la consulta_

A continuación definiremos estilo de la capa del tipo "Polígonos invertido" en la pestaña Estilo de propiedades. Podremos jugar con los colores de relleno para definir el color de la máscara.

[![mascara_propiedades_estilo](https://camo.githubusercontent.com/6ba5a102f91fbf508310bfa944a19b2a0b48548f/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353536392f31353034313930343731325f626239353236336432395f7a2e6a7067)](https://camo.githubusercontent.com/6ba5a102f91fbf508310bfa944a19b2a0b48548f/68747470733a2f2f6661726d362e737461746963666c69636b722e636f6d2f353536392f31353034313930343731325f626239353236336432395f7a2e6a7067)

_Propiedades del estilo Polígnos invertidos_

Una vez realizado esto y jugando con la activación/desactivación de capas podremos obtener el resultado que deseemos.

[![03_02_mascara_elsalado](https://camo.githubusercontent.com/9b4f97650cf84d18c2b5fa23d220e4f3b7ecd072/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333834382f31353034323236333134355f633531356664633330395f7a2e6a7067)](https://camo.githubusercontent.com/9b4f97650cf84d18c2b5fa23d220e4f3b7ecd072/68747470733a2f2f6661726d342e737461746963666c69636b722e636f6d2f333834382f31353034323236333134355f633531356664633330395f7a2e6a7067)

_Resultado_

Si estáis interesados también podéis acceder al tutorial [Creación de máscara de visualización con estilo de polígonos invertido con QGIS 2.4](http://youtu.be/t55Olt3tazs) en YouTube
        