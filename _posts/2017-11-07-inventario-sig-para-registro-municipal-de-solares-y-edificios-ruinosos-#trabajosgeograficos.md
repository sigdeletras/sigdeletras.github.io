---
title:  "Inventario SIG para Registro Municipal de Solares y Edificios ruinosos #trabajosgeográficos"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201711_rmse/inventario_por_edificacion.PNG"
categories: 
  - 2017
tags:
  - Consultoría geográfica
  - Urbanismo
  - Córdoba
---

Bajo la etiqueta [#trabajosgeográficos](twitter) voy a iniciar una serie de textos centrados en la exposición de algunos de los trabajos que he realizado en estos últimos meses. El motivo de estas entradas en la web es doble.

- Revisando las últimas entradas, he apreciado que están principalmente centradas en dos de los servicios que ofrezco: formación/divulgación y trabajos informáticos basado en las TIG (SIG, webmapping o geodesarrollos con Python). Es, sin embargo, el ámbito de la **consultoría geográfica** donde estos últimos meses han surgido más proyectos, por lo que creo que es un buen momento (y una buena estrategia) para darlos a conocer.
- Aunque parece que el tema se ha enfriado un poco, hace unos meses se pudo leer en distintos medios la noticia sobre la [desaparición del Grado de Geografía de la Universidad de Castilla-La Mancha](http://www.clm24.es/articulo/ciudad-real/uclm-no-ofertara-grado-geografia-profesores-alumnos-oponen/20170209194909146620.html). Han sido varias las manifestaciones y posiciones en contra tanto de alumnos y profesores, [colegios de geógrafos nacionales](http://cadenaser.com/emisora/2017/05/15/ser_toledo/1494866281_561732.html?ssm=tw) y de varios [profesionales del sector](https://gersonbeltran.com/2017/02/15/10-trabajos-que-hace-un-geografo/). Si con estas entradas puedo ayudar a un mejor conocimiento de la labor profesional del geógrafo, pues bienvenidas sean.


# Definición y objetivos del trabajo.

El objetivo principal del proyecto es la *recopilación, tratamiento y depuración de fuentes de datos para la generación de una base de datos georreferenciada que incluya el inventario de solares y edificios ruinosos del Casco Histórico de Córdoba*. Gracias al trabajo se pretendía tener un primer acercamiento a esta realidad urbanística y que sirviera de base para la futura redacción y puesta en marcha de la correspondiente Ordenanza municipal reguladora del Registro Municipal de Solares y Edificaciones Ruinosas. El trabajo fue realizado para la Oficina del Casco Histórico de la Gerencia Municipal de Urbanismo de Córdoba. 

# Marco teórico y legislativo.

El Registro Municipal de Solares y Edificaciones Ruinosas es un registro público de carácter administrativo, de competencia municipal y contemplado en el ordenamiento jurídico como un instrumento para el fomento de la edificación en suelo urbano eliminando la imagen prolongada de abandono que en “ciudad” proyectan las edificaciones ruinosas y solares. En Andalucía, la regulación vigente del Registro Municipal de Solares se contiene en los artículos 150 y siguientes de la [Ley 7/2002, de 17 de diciembre, de Ordenación Urbanística de Andalucía (LOUA)](https://www.boe.es/buscar/act.php?id=BOE-A-2003-811), modificada mediante Ley 2/2012, de 30 de enero. La Ley establece la obligación de los propietarios de iniciar, en el plazo otorgado a tal efecto por el planeamiento la edificación de las parcelas y solares, incluidos los que cuenten con edificación deficiente o inadecuada y la de ejecutar obras de restauración en aquellos edificios que cuenten con declaración legal de ruina urbanística. La no iniciación de la edificación en el plazo fijado al efecto para las distintas zonas de la ciudad, el incumplimiento de los deberes de conservación y rehabilitación y la declaración legal de ruina urbanística comportan la inclusión del inmueble en el Registros Municipal.

Por otra parte, una vez incluidos en dicho Registro Público, si los propietarios persisten en el incumplimiento del deber de rehabilitar/edificar, las fincas se declaran en situación de “venta forzosa” para su ejecución por sustitución del propietario incumplidor, mediante “concurso público”. Corresponde a los Ayuntamientos la competencia para crear y gestionar estos registros administrativos, así como, fiscalizar el cumplimiento de los deberes urbanísticos por los particulares incluyendo en el Registro las fincas de su término municipal incursas en edificación o rehabilitación forzosa. Esta labor municipal se plasma en el desarrollo y aprobación de la correspondiente Ordenanza Municipal.

# Fases del proyecto

## Análisis y normalización de datos

El punto de partida del proyecto consistió en el análisis y normalización de varias fuentes de información y trabajos de campo ya existentes. En este punto el trabajo con bases de datos fue fundamental, ya que permitió la estandarización de las diferentes fuentes y la creación de un primer modelo de datos para el inventario. La identificación de la unidad geográfica de análisis, en este caso la parcela catastral, fue relevante tanto para la georreferenciación de los registros ya existentes como para la contrastación con las capas catastrales del Casco Histórico, que pasó a ser la base del inventario inicial.

![Trabajos de depuración. Contrastación con catastro](/images/blog/201711_rmse/depuracion_catastro.PNG)

*Trabajos de depuración. Contrastación con catastro*

## Diseño del modelo de datos.

Para una mejor definición del modelo de datos, y teniendo en cuenta que los registros servirán de base para el futuro Registro Municipal de Solares y Edificaciones Ruinosas, fueron consultadas distintas ordenanzas en vigor en Andalucía (Sevilla, Puerto de Santa María o Almería). En dichas ordenanzas se pudo distinguir un primer grupo de atributos que describen la finca y otra serie de atributos vinculados a la gestión del registro, preceptos legales y /o reglamentarios. 

Debido a las características de este trabajo, nos centramos en los campos descriptivos de la finca, que con pequeñas variaciones a los que se le añadieron otro conjunto tanto de control (origen de la información) como de orientados al posterior análisis de los datos (superficies, dirección normalizada, sección censal, códigos de zona, distrito y barrio).

## SIG Inventario RMSE

Algunos de los trabajos que se realizaron en esta fase fueron:

- **Generación de dato único**. Una vez normalizados los datos de las distintas fuentes se procedió a la unión de los registros una única capa. Tras su tratamiento se generó el registro único al que se acompaño con su correspondiente informe (por fuentes de procedencia, por repeticiones). 

![Ejemplo de temático](/images/blog/201711_rmse/inventario_por_edificacion.PNG)

*Ejemplo de temático*

- **Definición de estructura de capas**. Junto las capas principales del trabajo se han incorporado otras fuentes cartográficas de referencia (Catastro, Ortofotografía) que ayuden al acceso, consulta y mantenimiento de los datos principales. Para la preparación de algunas de ellas fueron necesarios trabajos de conversión de CAD a SIG. Igualmente, se diseñaron un conjunto de temáticos orientados al análisis de esta primera carga de información (índices de edificabilidad, inventario por barrios, temático por tipo de protección, etc). Todas las capas del proyecto se encuentran proyectadas en ETRS89 UTM30 y almacenadas en una base de datos en geográfica.

![Capas de Referencia. Planos CAD de Edificación PEPCH](/images/blog/201711_rmse/capa_referencia.PNG)

*Capas de Referencia. Planos CAD de Edificación PEPCH*

- **Diseño de herramientas SIG de apoyo**. Con el fin de facilitar al máximo la consulta se diseñaron distintas salidas gráficas basadas en plantillas automáticas (Atlas). Dentro del SIG se diseño de formulario de consulta personalizado al que se le añadieron herramientas de edición (altas y bajas) programados con Python con su correspondiente respaldo en base de datos. Por último, comentar que también se habilitó una herramienta de callejero/portalero circunscrito al ámbito del proyecto basado en el proyecto CDAU de la Junta de Andalucía.

![Herramintas de consulta. Datos de Catastro](/images/blog/201711_rmse/acceso_catastro.PNG)

*Herramintas de consulta. Foto de fachado según de Catastro*

# Conclusiones

Aunque parte del trabajo se ha centrado en la explotación de las herramientas incorporadas en los SIG, es necesario tener en primer un conocimiento sobre la base teórica sobre el objetivo principal el trabajo. No son pocos los proyectos vinculados con la gestión y planificación urbanística de las ciudades en los que el papel del geógrafo es fundamental sobe todo por el conocimiento de las instrumentos de planificación como de los datos geográficos para poder llevarlos a cabo. 

Para cualquier duda o consulta más concreta sobre el trabajo no dudéis en ponerse en contacto conmigo.
