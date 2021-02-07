---
title:  "Cómo colaborar en proyectos de código haciendo Pull Requests"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202102_pr/04_pr.png" 
categories: 
  - 2021
tags:
  - desarrollo web
  - git
---

Los fines de semana intento sacar hueco para poder trabajar en proyectos personales, profundizar sobre alguna tecnología con la que esté trabajando o dedicar un rato a ver algunos de los vídeos de mi larga lista “Ver más tarde” de YouTube.

Desde que empecé aprender a usar la librería React para proyectos como [BuscaCalles](http://sigdeletras.com/2020/buscacalles-aplicacion-react-para-la-consulta-de-datos-de-cartociudad/) o al campo de los [mapas](http://sigdeletras.com/2020/side-project-desarrollo-de-aplicacion-web-con-react-y-leaflet-i/), las retransmisiones y vídeos del desarrollador [Miguel Ángel Durán](https://github.com/midudev), conocido como [@midudev](https://twitter.com/midudev) han ocupado alguno de estos ratos.


Uno de los proyectos recientes de Miguel Ángel ha sido la creación de una **covid-vacuna una aplicación web hecha con React que muestra el estado y progreso de la vacunación en España es contra el COVID-19 utilizando datos públicos**.  El proyecto se encuentra en [GitHub](https://github.com/midudev/covid-vacuna) y está abierto a colaboraciones. Y ha tenido cierta [repercusión en medios digitales](https://www.20minutos.es/noticia/4552926/0/lanzan-una-web-con-datos-del-gobierno-que-permite-ver-como-avanza-en-espana-la-vacunacion-contra-el-coronavirus/).

![covid_app.gif](/images/blog/202102_pr/covid_app.gif)
https://covid-vacuna.app/

Tenía ganas de revisar el código de la aplicación ya que seguro que iba a aprender bastante. De paso, si surgía algún aspecto en el que pudiera contribuir, me parecía una buena labor poder añadir un granito de arena sobre todo por la utilidad de la aplicación.

A priori, había pensado hacer alguna aportación al tema de los mapas, pero me di cuenta que la funcionalidad de descargar el JSON con los datos más recientes no cumplía con su misión, así que decidí profundizar en esta mejora.

Una vez desarrollado el código he usando GitHub para hacer un Pull Request a la espera tener el visto bueno para que se incorpore a la aplicación. De aquí ha surgido la idea de esta entrada centrada en los **pasos a seguir para poder colaborar en un proyecto de código abierto usando Git y GitHub**.

## ¿Qué es un Pull Request?

Dentro de la terminología de los sistemas gestores de versiones un **Pull Request** *es una petición que el propietario de un fork de un repositorio hace al propietario del repositorio original para que este último incorpore los commits que están en el fork*. 

Voy a exponer los pasos que he realizado para que se añadan las mejoras a la aplicación de Miguel Ángel. Seguro que así quedará bastante más claro este concepto.

## Realizar un fork

Un **fork o bifurcación** es una copia del código original del proyecto original. Esto nos va a permitir trabajar sin problemas en la aplicación, y si la cosa llega a buen fin, poder hacer el correspondiente  *Pull Request* para que los cambios se incorporen de nuevo al original (*merge* o 'mergeo' de toda la vida).

Partimos de la base de que tenemos una cuenta en GitHub. Para realizar un *fork*, debemos acceder a la URL donde se encuentra en repositorio original https://github.com/midudev/covid-vacuna. En la esquina superior derecha se encuentra el botón para realizar el *fork*.

![01_fork.png](/images/blog/202102_pr/01_fork.png)

Tras completar los pasos, podemos comprobar que ahora tenemos copia del repositorio en nuestra cuenta de GitHub.

![03_fork_sigdeletras.png](/images/blog/202102_pr/03_fork_sigdeletras.png)

## Guía de contribución

Si queremos que nuestra colaboración se acabe incorporando en el proyecto original,  debemos tener en cuenta los criterios que para ello ha establecido el autor para ello.

Miguel Ángel ha añadido información de las [características que deben tener los Pull Requests](https://github.com/sigdeletras/covid-vacuna#aceptas-pull-request) para que lleguen a buen puerto. Pero podemos decir que, cualquier proyecto de código abierto, debe tener su correspondiente guía de contribución. Muestras de esto en proyectos o librerias de mapas son la guía de [Leafet](https://github.com/Leaflet/Leaflet/blob/master/CONTRIBUTING.md), [pgRouting](https://pgrouting.org/docs/howto/contribute.html) o de [Python.](https://devguide.python.org/) 

## Flujo básico de Git

Mi objetivo en esta entrada no es entrar en explicaciones sobre cómo aplicar Git en nuestros proyectos. A pesar de ello, pienso que es fundamental seguir unos determinados pasos para sacarle el máximo partido a Git.

1. Tras realizar el fork, realizamos un **git clone** en nuestro equipo para tener una copia local.

```
git clone https://github.com/midudev/covid-vacuna.git
```

2. Según la documentación que consultes, se recomienda realizar una rama donde ir creando los cambios y añadiendo el nuevo código.  Las **ramas o branchs** permiten crear secciones de código que puedes trabajar en un entorno aislado. Esto quiere decir que lo que hagas en un *branch* no necesariamente afecta al código original. En esta ocasión, no he seguido esta pauta y he guardado los cambios en la rama principal (main) de mi proyecto local.


3. Para ir documentando cada cambio que vayamos añadiendo se usan los **commits**. Cada vez que añadimos un *commit* se crea una marca temporal del estado del código en ese momento. Se añade un texto descriptivo, por lo que es fundamental redactarlo de forma correcta. Cuando hagamos el PR se presentarán el listado de *commits* hechos. Estos datos darán información al dueño o responsable del repositorio sobre el objetivo de nuestra aportación. Antes de crear un *commit*, debemos añadir los ficheros al control de versiones con *git add*. Podemos indicar el nombre del archivo a añadir o usar punto  para añadirlos todos. Una vez añadidos, guardamos el cambio con *commit*.

```
git add .
git commit -m "Added the new component DownloadJson"
```

4. Hasta ahora estamos trabajando en el repositorio local que hemos clonado. Pero para poder realizar el *Pull Request* debemos subir los cambios a nuestro repositorio remoto con **push**.

```
git push origin main
```

## ¿Hacemos un PR?

Ya está todo preparado para hacer un *Pull Request*. Esto es realmente sencillo en GitHub ya que incluye un apartado específico para ello.

![04_PR.png](/images/blog/202102_pr/04_PR.png)

El *Pull Request* debe ir acompañado con la información necesaria para que se pueda comprender en qué consiste el trabajo, por qué se ha realizado y qué aportada.En GitHub se presentan también el listado de *commits* para que sean revisados. De ahí la importancia de comentarlos adecuadamente.

![04_PR_info.png](/images/blog/202102_pr/04_PR_info.png)


## Dudas, preguntas y mejoras

Lo bueno que tienen los PR es que antes de ser aprobados o 'mergeados' dan la posibilidad de entablar una conversación entre el autor y la persona que los ha realizado. 

En mi caso, [Miguel hizo unas sugerencias acertadas sobre la posibilidad de aprovechar propiedades](https://github.com/midudev/covid-vacuna/pull/124) ya creadas y que dieron pie a añadir unos cambios de código y otras mejoras.

En esta dirección se puede serguir el hilo https://github.com/midudev/covid-vacuna/pull/124

## Para terminar

El paso final, si el responsable del proyecto lo cree oportuno es que se añada nuestro aporte al proyecto original. Mientras escribo esta entrada el PR está revisado y pendiente de ser añadido a la aplicación.

Este es un ejemplo sencillo de las grandes posibilidades de aplicar licencias abiertas a nuestros proyectos y abrir la opción de que otros desarrolladores hagan contribuciones en el código.

Proyectos como el realizado por *@midudev* son sin duda una **buena oportunidad para probarnos como desarrolladores y añadir el hábito de colaborar en iniciativas tan interesantes**.


