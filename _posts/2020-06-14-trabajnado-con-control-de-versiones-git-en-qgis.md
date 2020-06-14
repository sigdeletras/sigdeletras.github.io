---
title:  "Trabajando con control de versiones Git en nuestros proyectos QGIS"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202006_git/portada.png" 
categories: 
  - 2020
tags:
  - qgis
  - git
---

## Qué es un sistema de control de versiones

Un **sistema de control de versiones** (VCS por sus siglas en inglés) es una aplicación informática que registra los cambios realizados en un archivo o conjunto de archivos digitales a lo largo del tiempo.

Gracias a la puesta en marcha de un sistema de control de versiones podremos por ejemplo:

- Regresar a versiones anteriores de nuestros archivos.
- Comparar cambios a lo largo del tiempo.
- Identificar quién modificó por última vez algo que pueda estar causando conflictos y resolverlo.
- Permitir que varias personas estén trabando en versiones (ramas) del proyecto
- Unir cambios realizados por diferentes usuarios sobre los mismos ficheros.

Todos en algún momento de nuestra vida "informática" hemos hecho control de versiones "casera" de nuestros programas. Con el miedo a no perder nuestros datos, o para probar distintas mejoras hemos copiado y renombrado nuestros ficheros usando algún sistema más o menos trabajado (archivo_final, archivo_final2, archivo_final22, archivo_final_final...)

![Camiseta](/images/blog/202006_git/0_versiones.jpg)

Esta ¿metodología? puede sernos de utilidad hasta cierto momento, pero en un ámbito profesional no es sin duda la forma de trabajar más correcta.

El uso de **un sistema de versiones es fundamental en cualquier proyecto de desarrollo**, ya sea dentro de una empresa IT o como metodología de trabajo de un proyecto personal. A día de hoy mi trabajo se mueve entre la consultoría GIS y el desarrollo web, por lo que voy a intentar explicar **cómo  aplicar estas herramientas en la gestión de un proyecto geo usando el Sistema de Información Geográfico QGIS**.

## Git, GitHub, Bitbucket, GitLab...


Los VCS han evolucionado a lo largo del tiempo. Actualmente se suele trabajar con sistema de control de versiones distribuidos, en los que los clientes (usuarios) no sólo descargan la última instantánea de los archivos sino que replican completamente el repositorio. Esto supone una mejora sobre los sistemas centralizados ya que existen varias copias listas para restaurar del proyecto, obteniendo más seguridad con ello.

Dentro de este tipo, sin duda [Git](https://es.wikipedia.org/wiki/Git) diseñado por Linus Torvalds, es el más conocido y usado.

Cuando se está empezando con todo esto, muchas personas confunden Git con GitHub. **Git** es software que permite establecer un sistema de control de versiones, mientras que [GitHub](https://github.com/) es una plataforma que ofrece un grupo de servicios que facilitan el uso de Git, como por ejemplo hosting de proyectos, facilidades de colaboración, reviews de código, perfiles personales, pull requests, issues, etc.

Además de GitHub, existen otras plataformas igual de potentes como [Bitbuckets]() o [GitLab](). Cada una tiene sus fortalezas, por lo que que en este sentido cuadra perfectamente la socorrida frase "sobre gustos...".

Para poder comenzar a montar nuestro control de versiones en local solo necesitamos tener instalado Git.

## Usando Git en nuestro proyecto QGIS

Vamos a aplicar un sistema de control sobre un proyecto QGIS. El objetivo es controlar todos los archivos que se encuentren dentro de una carpeta de proyecto. Esto quiere decir, que podremos hacer seguimiento no solo del fichero de proyecto de QGIS, sino de todos los ficheros dentro de esta carpeta. 

A pesar de esto, hay que comentar que **toda la funcionalidad de usar Git se efectuarán sobre ficheros planos o de texto tipo (qgs, txt, csv, xml, geojson, sld...)** ya que el sistema va a poder incluso indicarnos que líneas han cambiado. Para los ficheros binarios (jpg, tif, doc, shp, dbf..) solo controlaremos que han sido añadidos. 

Lo bueno de todo esto es que los proyectos QGIS pueden ser guardados como archivos de texto plano, ya que **el fichero con la extensión qgs  de QGIS es fichero de marcas**, como pueden ser un archivo html o xml. Al usar este formato de proyecto, frente a la opción de proyectos  comprimidos con extensión ***.qgz** (archivo comprimido, por lo tanto binario), perderíamos la opción de almacenar datos auxiliares pero por otro lado podemos controlar más los cambios que se realicen.

Si queremos modificar la opción por defecto con la que se guardan los proyectos en QGIS, accedemos al menú *Configuración>Opciones* y lo indicamos en la pestaña General.

![img/proyectos_qgis.png](/images/blog/202006_git/proyectos_qgis.png)

## Iniciando el control del versiones

El primer paso que debemos hacer es descargar e instalar Git en nuestro equipo según nuestro sistema operativo.

![download_git.png](/images/blog/202006_git/download_git.png)

Podemos manejar Git desde la terminal o consola de nuestro equipo. Si no estamos acostumbrados a manejarnos con comandos podemos usar alguno de los [clientes](https://git-scm.com/downloads/guis/) que nos aportan una interfaz gráfica para ello como puede ser [Github Desktop](https://desktop.github.com/), Git Gui, [GitKraken](). 

Otra opción es controlar Git mediante nuestro editor de código de cabecera. En mi caso, cuando estoy con desarrollos web, uso **Visual Studio Code**.

Cada uno puede elegir el que más interese pero para esta entrada vamos a usar directamente la consola (Linux).

Para iniciar el control de versiones, accedemos a nuestra a la carpeta del proyecto (ej. /gis_project), abrimos la consola y ejecutamos el siguiente comando de git

```
git init
```

Al ejecutar este comando, se creará un nuevo subdirectorio oculto *.git* en nuestra carpeta de trabajo. También se creará una rama maestra (master). Una **rama o branch** es un espacio o  área de trabajo independiente que será controlado por nuestro sistema.

![01_init.png](/images/blog/202006_git/01_init.png)

## Añadiendo archivos con Git

Vamos a crear un proyecto QGIS sencillo en nuestra carpeta. Dentro del proyecto vamos a cargar la capa de países de [Natural Earth](https://www.naturalearthdata.com/downloads/10m-cultural-vectors/10m-admin-0-countries/) que se ubicará dentro de la carpeta */data*. 

Para que se apliquen los cambios debemos guardar nuestro proyecto QGIS.

![02_countries.png](/images/blog/202006_git/02_countries.png)


Ahora vamos a ver el estado de seguimiento de los archivos de nuestro directorio o repositorio desde la terminal. El comando *git status* nos ayudará para este cometido. Al ejecutarlo nos informará sobre qué archivos están modificados y sin seguimiento y cuáles con seguimiento pero no confirmados aún.

![03_git_status.png](/images/blog/202006_git/03_git_status.png)

El sistema nos está indicando que tenemos archivos cuyo estado no está siendo seguido. Para incluirlos todos usamos *git add .*. Y volvemos a ejecutar *git status*

![04_git_add_status.png](/images/blog/202006_git/04_git_add_status.png)

Vemos que los archivos que conformar le shape de países y el proyecto están añadidos pero deben ser confirmados. Esto lo realizamos  con el comando *git commit*. Añadimos el parámetro *-m* a la ejecución del comando para añadir un comentario sobre este acción en la misma ejecución.

```
git commit -m 'QGIS Project created and countries layer added'
```
Vamos a realizar algunas modificaciones. Por ejemplo, añadimos un título al proyecto, cambiaremos la simbología de la capa y creamos un marcador espacial centrado en España. Cada vez hagamos un cambios, salvamos el proyecto y realizamos un *git commit*. Poco a poco vamos a ir creando un historial de cambios, que tendremos a mano para poder ser restaurado si es necesario.

Git posee el comando *diff* para poder comparar distintas versiones de nuestros datos. Pero aquí **es bastante más interesante usar algunos de los programas que dotan de interfaz gráfica al trabajo con este control de versiones**. Visual Studio Code permite gestionar con las versiones de nuestros proyectos. En la siguiente captura puede verse una comparativa del proyecto de QGIS después de añadir el marcado espacial.

![06_diff.png](/images/blog/202006_git/06_diff.png)

## Trabajando con ramas

Un aspecto más avanzado y potente es el trabajo con versiones. Supongamos que en nuestro proyecto trabajan dos personas y que una de ellas se va a encargar del diseño de las composiciones del mapa. Para que los dos puedan estar trabajando de forma simultánea sobre mismo proyecto vamos a trabajar con ramas. 

Necesitamos crear una "copia" del proyecto, lo que en terminología git se llama una rama o branch, para el técnico trabaje sobre ella creando las composiciones de mapas. Tras realizar el diseño de las salidas gráficas, todos los cambios que realicen serán unidos (merge) a la rama principal (master).

El usuario que tiene acceso al proyecto, por ejemplo en una carpeta compartida o en un repositorio remoto como Github, va a crear su rama de trabajo que se llamará "layouts" usando el comando *git checkout -b "layouts"*. 

Podemos comprobar el listado de ramas creadas con *git branch -a*

![07_checkout.png](/images/blog/202006_git/07_checkout.png)

Tras realizar la composición y gestionar los cambios en el sistema (add, commit...), el objetivo es actualizar la rama principal con los nuevas composiciones creadas. Los pasos a seguir son:

- Nos posicionamos en la rama principal (master) con *checkout*

```
git checkout master
```
- Y ahora añadiremos los cambios realizados en la rama "layouts" con merge.

```
git merge layouts
```

## Es no es todo amigos...

Hemos visto los aspectos más sencillos para comenzar a aplicar el sistema de control de versiones Git en nuestros proyectos de QGIS. Pero hay un sinfín de opciones que van a generar nuestros trabajos SIG. Podemos resolver diferencias entre ramas, generar un fichero para "ignorar" el control de determinados archivos  o carpetas que no van a modificarse, trabajo con repositorios remotos...pero todo esto lo dejamos para otra entrada.

