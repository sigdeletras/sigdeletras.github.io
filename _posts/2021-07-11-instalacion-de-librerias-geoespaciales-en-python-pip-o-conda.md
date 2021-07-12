---
title:  "Instalación de librerías geoespaciales en Python. ¿Pip o Conda?"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/202107-pip-conda/04_jupiter.jpg" 
categories: 
  - 2021
tags:
  - python
  - anaconda
---

Python, junto a R, es uno de los lenguajes de uso más frecuente en el ámbito SIG. Este lenguaje de programación suele ser la primera opción para comenzar a programas de aquellas personas que trabajan en el ámbito del análisis geoespacial. 
<!--more-->

Entre las razones de esta elección, además de su rápida curva de aprendizaje, se encuentra su integración como lenguaje de scripting en SIG de escritorio tan conocidos como QGIS o ArcGIS.

Pero el uso de Python en el campo de las geotecnologías no se limita explotación dentro de un SIG. Gracias a la cantidad de librerías existentes (ej. GDAL/OGR, Geopandas,  Shapely, Rasterio, Fiona, PyProj, Numpy, Pandas, Scipy Matplotlib…) podemos obviar la interfaz gráfica que nos ofrecen los SIG y trabajar directamente con los datos espaciales para su consulta, edición y análisis. 

La facilidad de acceso a grandes volúmenes de datos y el auge de las tecnologías y salidas profesionales (*data scientist*) relacionadas con el aprendizaje automático, la visualización de datos, el procesamiento de imágenes o el procesamiento ETL en el que se incluye el dato geográfico está provocando un acercamiento aún mayor a Python.

Dejando aparte el interés y las razones del uso de Python en ámbito profesional geo, **el aprendizaje de un nuevo lenguaje informático pasa siempre por su instalación**. 

En la siguiente entrada voy a dejar comentados algunos **aspectos para tener en cuenta si queremos empezar a manejar Python y sus librerías SIG**.

## Instalación de Python

Python se encuentra preinstalado en máquinas con GNU/Linux. Abriendo una consola de comandos y escribiendo python  o python3 nuestro equipo está preparado para empezar a programar.

Para equipos con Windows tenemos que realizar la descarga de los instaladores según la arquitectura de nuestro equipo desde web de Python [https://www.python.org/](https://www.python.org/) y proceder a su instalación.

![Hello World Python](/images/blog/202107-pip-conda/00_python_hellworld.jpg)

No trabajo con MacOS, pero según leo, creo que viene  preinstalado Python 2.7 por lo que será también necesario realizar la instalación a Python 3.

## Paquetes y entornos virtuales.

Al instalar Python en nuestro equipo tenemos disponibles por defecto un conjunto de módulos y paquetes destinados a cubrir las operaciones más comunes de la programación diaria.

A estos paquetes o librerías se suman sin embargo otros módulos desarrollados por la comunidad de programadores de Python. La mayoría de ellos se encuentran alojados en el [repositorio de software PyPI](https://pypi.org/).

![Pypi](/images/blog/202107-pip-conda/01_pypi_gdal.jpg)
 
Para instalar un módulo, utilizaremos el [administrador de paquetes Python pip](https://es.wikipedia.org/wiki/Pip_(administrador_de_paquetes)) usando el comando *install*.

En el siguiente comando se instalaría de forma global la librería [rasterio](https://rasterio.readthedocs.io/en/latest/) para el trabajo de archivos ráster.

```
pip install rasterio
```

Hasta ahora parece todo muy sencillo. Pero hay que tener en consideración varios aspectos.

- Las **librerías tienen versiones y la mayoría de ellas tienen dependencias** a otras librerías. Por ejemplo, para usar el paquete de tratamiento de datos espaciales [Geopandas]( https://geopandas.org/) deberemos tener instalado también en nuestro equipo las versiones correctas de numpy, pandas, shapely, fiona y pyproj.
- Si hacemos una instalación de forma global **solo podremos tener una versión concreta instalada de un determinado módulo***

Para dar solución a estos aspectos es recomendable el uso de **entornos virtuales**.

Un entorno es un espacio donde instalará los paquetes necesarios para el desarrollo de un determinado proyecto. El uso de entorno solucionará el tema de los requisitos y dependencias y permitirá la elección de las versiones que necesitemos.

Con pip, podemos instalar *venv* o *virtualenv* que van a darnos la opción de crear entornos virtuales.

En el siguiente código creamos con *venv* un entorno que llamaremos 'geoenv', lo activamos e instalamos la librería [Shapely](https://pypi.org/project/Shapely/).

![Creación de entorno virtual con venv](/images/blog/202107-pip-conda/02_venv.jpg)

## Conda y Anaconda al rescate

Aunque pip es una magnífica herramienta para instalar paquetes, en algunas ocasiones, debido a las dependencias, **las instalaciones no son exitosas**. Instalar por ejemplo el paquete GDAL o Geopandas es un auténtico quebradero de cabeza.

![Error a instalar geopandas con Pip](/images/blog/202107-pip-conda/03_error_geopandas.jpg)
 
Es aquí donde Anaconda y el instalador Conda vienen al rescate.

[Anaconda](https://www.anaconda.com/)  es una *suite* de código abierto multiplataforma que abarca una serie de aplicaciones, librerías y conceptos diseñados para el desarrollo de la ciencia de datos con Python y R.

Cuando instalamos Anaconda en nuestro equipo, además de contar con Python y R, tendremos un administrador de entornos, una interfaz gráfica de usuario (Anaconda Navigator) y un sinfín de librerías preinstaladas.

Anaconda dispone de su **propio administrador de paquetes** propio llamado **Conda**. Con Conda gestioanamos los entornos e instalamos o actualizamos los paquetes desde el repositorio de Anaconda. 

Los paquetes de Conda son binarios, por lo que no es necesario tener compiladores para instalarlos. Esto es una de las grandes ventajas respecto a pip y en la que muchas veces tropezamos al instalar nuestros módulos.

![Comparación Conda vs Pip](/images/blog/202107-pip-conda/comparación_conda_pip.jpg)
*Fuente: Anaconda web*

Si nos decantamos por la [instalación de Anaconda](https://www.anaconda.com/products/individual) podemos usar la interfaz gráfica de Anaconda Navigator para crear e instalar paquetes o bien usar el terminal Anaconda Promt (Windows) o directamente el terminal (Linux y macOS) para las gestiones.

![Anaconda Navigator ](/images/blog/202107-pip-conda/anaconda_navigator.png)

## Miniconda

Instalar **Anaconda** nos va a permitir trabajar sin problemas en nuestros proyectos de Python y realizar las correspondientes tareas de administración y gestión. Pero tenemos un pequeño inconveniente. Esta **gran disponibilidad de recursos** ocupa aproximadamente 3GB.

Como alternativa a Anaconda, con un peso mucho menor (400 MB) y con una instalación limitada a los imprescindible tenemos [Miniconda](https://docs.conda.io/en/latest/miniconda.html)  que instalará el gestor Conda y a sus dependencias.

En mi opinión prefiero tener controlado los paquetes que uso en cada proyecto, por lo que me decanto por Miniconda.

## Un ejemplo de trabajo con datos ráster con Conda

Voy a mostrar continuación un breve guion de gestión de un **proyecto Python con Conda para trabajar con un archivo de modelos digital de elevaciones** del IGN. 

Nuestro proyecto va a requerir la instalación de las siguientes librerías:

-	Rasterio
-	[Matplotlib](https://matplotlib.org/) para el ploteo del archivo

Usaremos  como entorno interactivo para trabajar [Jupiter Lab](https://jupyter.org/).

- Tras instalar Miniconda lo primer que debemos hacer es crear un *enviroment* y activarlo.
  
```
conda create --name geoenv
conda activate geoenv
```

- El siguiente paso será la instalación de las librerías. 

```
conda install rasterio matplotlib 
```

- Y necesitaremos también Jupiter Lab pero usando el repositorio [conda-forge](https://conda-forge.org/)

```
conda install -c conda-forge jupyterlab
```

- Tras las instalaciones lanzaremos Jupiter y ya tendremos todo listo para ir creando nuestro código Python.

```
jupyter lab
```

La siguiente captura muestra un código muy sencillo para comenzar nuestro proyecto de visualización de un MDE en Python.

![Anaconda Navigator ](/images/blog/202107-pip-conda/04_jupiter.jpg)

```python
import rasterio
from matplotlib import pyplot

data = rasterio.open("data/PNOA_MDT25_ETRS89_HU30_0923_LID.asc")

print ('-------Metadatos-------------')
print ('Formato de datos:', data.driver)
print (f'Número de bandas: {data.count} ')
print (f'Ancho de imagen: {data.width} ')
print (f'Altura de imagen: {data.height} ')
print (f'Rango geográfico: {data.bounds}')
print ('-------Estadísticas-------------')
band1 = data.read(1)
print (f'Elevación máxima: {band1.max ()}')
print (f'Elevación mímina: {band1.min ()} ')
print (f'Media: {band1.mean ()}')

pyplot.imshow(data.read(1), cmap='pink')
pyplot.show()
```
Como hemos podido apreciar comenzar a usar Python sin la ayuda de un Sistema de Información Geográfica no es realmente complicado. El campo de aplicación y las aplicaciones para el análisis geográfico es enorme.