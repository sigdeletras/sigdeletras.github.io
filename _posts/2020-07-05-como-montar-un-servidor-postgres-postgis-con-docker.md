---
title:  "Coomo montar un servidor Postgres-PosGIS con Docker"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202007_docker/portada.png" 
categories: 
  - 2020
tags:
  - docker
  - postgres
  - postgis
  - pgrouting
---

A día de hoy son varios los cursos que estoy dando dentro de la [oferta formativa de Geoinnova](https://geoinnova.org/cursos/patricio-soriano/) en los que se tratan temas vinculados con **PostGIS**, la extensión geográfica de PostgreSQL. Los temas van desde aspectos básicos de bases de datos relacionales con  PostgreSQL hasta prácticas avanzadas usando la extensión de redes **pgRouting**.

Dependiendo del sistema de operativo de los alumnos, hay veces en las que tenemos que usar distintas versiones de la base de datos y/0 de sus extensiones geográficas. Esto lleva a que se planteen dudas técnica como por ejemplo la de instalar la extensión de pgRouting para equipos Mac o la de tener habilitados varios servidores de bases de datos.

Motivado por un [pasado tuit](https://twitter.com/pgrouting/status/1278498807836073984) desde la cuenta de [Twitter de pgRouting](https://twitter.com/pgrouting?lang=es) donde se comentaba que se iba a mantener la imagen oficial de a extensión de redes para Docker, he pensado que sería interesante hacer una **guía sobre cómo instalar Docker y añadir una imagen/contenedor que permita usar distintas versiones de Postgres y de sus extensiones geográficas**.

![Love is in the air](/images/blog/202007_docker/portada.png)

Llevo tiempo usando con Docker en mi equipo con contenedores para PostgreSQL/PostGIS, Geoserver, nginx o Odoo y tras repasar la documentación del repositorio, me pareció lo suficientemente completa para animar al que le tenga curiosodad adentrarse en el mundo de la "dokerizanción".

Aunque trabajo con Linux, en esta ocasión **la instalación de Docker será para Windows** ya que es el sistema operativo que más suelen usar mis alumnos. Después de Windows el sistema operativo que más usan es macOS.

## Pero... ¿qué es Docker?

No se me ocurre una mejor descripción que la que usé hace algo más de una año en la entrada [A vueltas con Docker](https://medium.com/@pasoriano/a-vueltas-con-docker-f3e8e15b8f4a) que hice en Medium cuando empecé a usar Docker.

> “La idea detrás de Docker es crear contenedores ligeros y portables para que las aplicaciones software puedan ejecutarse en cualquier máquina con Docker instalado."

La definición está sacada de una charla [Nacho Álvarez](https://twitter.com/neonigmacdb) de Redsys.


## Instalación de Docker para Windows

Para la instalación de Docker en Windows simplemente he siguido los pasos de la guía [Get started with Docker for Window](https://docs.docker.com/docker-for-windows/) dispobible en la documentación oficial. 

Pensando de nuevos en mis alumnos, existe también una entrada  para [instalar Docker en Mac<](https://docs.docker.com/docker-for-mac/install/)

- Descargamos **Docker Desktop for Windows** desde la siguiente [dirección web](https://hub.docker.com/editions/community/docker-ce-desktop-windows/) e instalamos en el equipo.
- Podemos comprobar que todo se ha instalado correctamente abriendo la consola de comandos y ejecutando el comando
- 
```
docker -version
```

![01_docker_version.jpg](/images/blog/202007_docker/01_docker_version.jpg)

Al instalar **Docker Desktop for Windows** podremos seguir un breve tutorial que instala un contenedor demo y otras configuraciones. En principio no vamos a seguir el tutorial y pasamos directamente a montar nuestra imagen de PostgreSQL usando comandos en terminal por lo que estos pasos serviran para cualquier sistema operativo.


## Instalado  una imagen de Docker

Una imagen de Docker  es una especie de plantilla, una captura del estado de un contenedor. Podríamos decir que una imagen es como un snapshot de una máquina virtual, pero mucho más ligero.

Vamos a crear una imagen con el comando *run* en nuestro equipo con un Potsgres 11, PosGIS 2.5 y pgRouting 2.6.3. La imagen se llamar a *postgres11_25_263*, va a usar el puerto 5435 para conectarse a la base de datos y la contraseña será *postgres*.


```
docker run --name postgres11_25_263 -p 5435:5432 -e POSTGRES_PASSWORD=postgres pgrouting/pgrouting:11-2.5-2.6.3 
```

Si intentamos instalar nuetra imagen en Windows nos saldrá un error indicando que esta imagen no puede crearse ya que está basada en Linux.

![error](/images/blog/202007_docker/error_linux.jpg)

Para poder usar la imagen accedemos al menú de Docker Desktop y cambiamo el cliente de Docker con la opción *Switch to Linux containers...*

![02_linux.jpg](/images/blog/202007_docker/02_linux.jpg)

Ahora podremos ejecutar la instalación de nuestra imagen.

## Usando contenedores

Los contenedores son instancias en ejecución de una imagen de Docker. Son los que ejecutan nuestra aplicación con todos los recursos necesarios integrados. El concepto de contenedor es como si restauramos una máquina virtual a partir de un snapshot.

Esta opción es mi preferida ya que puedes definir en un archivo la configuración de la instalación. El [repositorio de Github de pgRouting](https://github.com/pgRouting/docker-pgrouting) están los archivos para instalar los contenedores según las versiones más recientes. 

Para poder usarlos podemos [descargar directamente el repositorio](https://github.com/pgRouting/docker-pgrouting/archive/master.zip) en formaro zip o mejor clonarlo usando Git.

Si vamos a usar Git (previamente instaladao en nuestro equipo) ejecutamos:

```
git clone https://github.com/pgRouting/docker-pgrouting.git
```

El paso siguiente será acceder a la carpeta de la versión que queramos instalar. 
Ahora vamos a montar un Postgres 12, con PostGIS 3 y la última versión de pgRouting. 

Accedemos a la carpeta correspondiente y localizamos el archivo *docker-compose.yml* para editarlo.

![03_folder.jpg](/images/blog/202007_docker/03_folder.jpg)

La única modificación que vamos a realizar es cambiar el número del puerto que se usará en el contenedor (5433)

![](/images/blog/202007_docker/04_compose.jpg)

Para terminar debemos abrir de nueva un terminar de comandos, acceder a la carpeta y lazar nuestro contonedor con *docker compose up*

![05_compose.jpg](/images/blog/202007_docker/05_compose.jpg)

# Conexiones a nuestros servidores con pgAdmin4.

La imagen y el contendor Docker que hemos usado son accesibles desde la ip 127.1.0.0 o localhost. La imagen usa el puerto 5435 y el contendor el 5433. 

Si usamos la interfaz gráfica de pgAdmin https://www.pgadmin.org/ vamos ahora a conectarnos nuestros dos nuevos servidores de datos.

En la siguiente captura está el ejemplo de la conexión al servidor del contendor.

![07_pgadmin](/images/blog/202007_docker/07_pgadmin.jpg)

Los pasos siguientes serán los de la creación de nuestra base de datos Postgres y los de añadir las extensiones geográficas PostGIS y pgRoutinng.

![07_extensiones](/images/blog/202007_docker/08_extensions.jpg)

