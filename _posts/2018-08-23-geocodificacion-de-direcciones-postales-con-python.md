---
title:  "Geocodificación de direcciones postales con Python"
excerpt_separator: "<!--more-->"
comments: true
related: true
header:
  teaser: "/images/blog/201808_geocoder/imgentrada.PNG" 
categories: 
  - 2018
tags:
  - Python
  - Geocodificación
---

Hace unos meses tuve que realziar un trabajo en el que era necesario la **georreferenciación de direcciones postales** de un numeroso conjunto de registros. Los datos formaban parte de una aplicación de expedientes administrativos que no contaba con un módulo geográfico, ni tampoco con un sistema normalizado de callejero implementado. **El objetivo de trabajo era dotar de componente territorial a la información para usarlos posteriormente en un análisis SIG vinculado con la planificación municipal en materia de vivienda**.

<!--more-->

Los datos de interés se encontraba dentro de la misma denominación del expediente. De manera más o menos repetitiva seguía una pauta: descripción del tipo específico de trámite seguido de la dirección postal o referencia directa al inmueble afectado y otros atributos relativos al expediente.

Cuando se incluye la dirección postal en un texto "abierto" la **formula más usada es *'tipo de via + nombre de via + número de portal'***. Lamentablemente al no contar un protocolo cerrado de edicion nos podemos encontrarnos "cien y una" **variantes**. Algunas de las más frecuentes son:

- Diferencias en las denominaciones de las vías (ej. *Calle La Plata-Plata, C/ José María Martínez-José Mª Castro*) o simplemente calles incorrectas.
- Uso de abreviaturas para identificar del tipo de vía (ej. *Calle-C/, Avenida-Avda, Pza-Plaza...*). El sistema de abreviaturas puede o no estar normalizado.
- Número de portal con o sin las abreviaturas ('nº', 'n.º'' o simplemente 'n')
- Referencias a varios inmuebles (ej *'Calle Jose María Valdenebro 37 y Calle Previsión 24'*)
- Uso del nombre del inmueble en en vez de su dirección (ej. *Iglesia de la Purificación, Hotel Conquistador...*)

Hay **otra serie de casuísticas** que podemos encontrar por ejemplo al indicar la ubicación de obras lineales en vía o vías públicas (ej. redes de abastacmiento o saneamiento, cableado, pavimentación...) por lo que no tienen número de portal (ej. *Pavimientación de la Calle Marte*). Tenemos también expedientes (probación de planeamiento, proyectos de urbanización, licencias de obras...) en zonas en proceso de urbanización y que por lo tanto no tienen dirección postal completa (ej. *Manzana A, Parcela 3 del Plan Parcial P2*). Por nombrar alguna más, hay  procesos administrativos en ámbitos no urbanos en los que es frecuente usar nombres geográficos o topónimos (*Paraje, Huerta de...*) 

Dejando a un lado estas ejemplos espaciales y especiales, **las variaciones en la descripción de la dirección pueden ser corregidas con bastantes garantías de éxito gracias a la informática**. La forma más común es la usar hojas de cálculo o bases de datos y, con mucha paciencia y tiempo, normalizar la información. Otra metodología sería la **diseñar, usando un lenguaje de porgramación como Python, *scripts* de búqueda y reemplazo** que se encargarán de automatizar estos arreglos y presentarnos los resultados tal y como nos sea de más entidad. 

En el proyecto al que hago referencia, una vez obtenido ficho fichero en formato CSV, se planteó la **metodología de geolocalización** que mayor y mejor número de resultados ofreciera. 

Las localizaciones obtenidas mediante **servicios de geocodifiación (ej. Google)** no fueron muy satisfactorio por lo que se optó por una solución más "clásica". De forma resumida, el trabajo final consistió en el enrriquecimiento de la información con el código del callejero del INE que permitió la unión de los registros con la capa geográfica del Callejero Digital Unificado de Andalucía mediante la combinación de *"códigoINE + nportal"*. Posteriormente se realizaron un conjunto de trabajos puramente SIG de asignación de refencia catastral a los registros.

Como era de esperar el número de coincidencias no fue total, pero **permitió disminuir el volumen de geolocalizaciones a realizar de forma manual**. Esto supuso una considerable reducción de los tiempos del proyecto.

He comentado que los resultados de la primera prueba de concepto en la que se probaron las APIS de geocodifición no fueron los esperados. A pesar de esto, la experiencia sirvió para analizar, documentar y valorar los usos de estos recursos en futuros encargos.

En esta entrada comentaré de forma muy simplifica **cómo usar estos servicios de geolocalización mediante la librería Geocoder de Python**.

## Usando librería Geocoder de Python para geocodificar direcciones postales

**[Geocoder](https://geocoder.readthedocs.io/) es una librería de Python** desarrollada por [Denis Carriere](https://twitter.com/DenisCarriere) **para realizar trabajos de geocodifiación** (obtener coordenadas a partir de una dirección) **y geocodificación inversa** (obtener dirección a partir de coordenadas) **mediante APIs de geocodificación** tales como Google, Nominatim, Bing, Yahoo, Here...

Antes de comenzar la librería debemos...

- Tener [Python](https://www.python.org/downloads/) ;-) y si es Python 3.* mejor que mejor....
- Instalar el módulo en nuestro equipo  o entorno virtual, por ejemplo usando el [instalador de paquetes pip](https://pypi.org/project/pip/)

Comenzamos importando el paquete Geocoder

```python
import geocoder
```
Una vez importada la librería podemos usar sus funciones. En la siguiente línea un ejemplo de geocodificación de una dirección usando el la [API de geocodificación de Google](https://geocoder.readthedocs.io/providers/Google.html).

```python
loc = geocoder.google('Calle El Almendro 6, Córdoba, Spain')
```

Podemos comprobar que la dirección ha sido indetificada imprimiendo la variale

```python
loc
<[OK] Google - Geocode [Calle el Almendro, 6, 14006 Córdoba, Spain]>
```

Para obtener las coordenadadas accedemos a los atributos

```python
loc.latlng
[37.8961199, -4.7830962]
```

Al presentarse como una lista, el acceso a la latitud y longitud de forma independiente se realiza mediante su índice.

```python
print('Latitud: {} Longitud: {}'.format(loc.latlng[0],loc.latlng[1]))
Latitud: 37.8961199 Longitud: -4.7830962
```

Podemos usar otros servicios de geocodifiación, por ejemplo [Nominatim de OpenStreetMap](https://nominatim.openstreetmap.org/). En este caso geocodificamos la dirección por el nombre del inmueble.

```python
loc1 = geocoder.osm('Hospital Universitario Virgen del Rocío, Sevilla, Spain')
loc1
<[OK] Osm - Geocode [Hospital Universitario Virgen del Rocío, Calle Antonio Maura Montaner, Tabladilla-La Estrella, Distrito Sur, Sevilla, Andalucía, 41005, España]>
loc1.latlng
[37.3629504, -5.97893023224876]
```
**La potencia de usar una lenguaje de programación es que podemos sistematizar operaciones repetidas creando un fragmento de código que haga este trabajo**. Así por ejemplo, nuestro programa podría leer el archivo CSV con el listado de direcciones, que buscara cada una de las direcciones usando la librería Geocoder y que nos devolviera las coordendas encontradas.

Añadimos el módulo CSV para trabajar con este tipo de archivos.

```python
import csv
```
Abrimos nuestro fichero *csv_in.csv* indicando el sistema de codificación del archivo. A continuación iteramos para ver los datos que posee.

```python
with open('csv_in.csv', encoding="utf8") as csv_file:
  csv_data = csv.reader(csv_file, delimiter=',', quotechar='\'')
  for row in csv_data:
    print(row)
```

    ['id', 'direccion', 'tipo']
    ['1', 'CALLE RONQUILLO BRICEÑO 10', '100']
    ['2', 'CALLEJA DEL POSADERO 21', '100']
    ['3', 'AVENIDA DEL MEDITERRÁNEO Y CALLE CANTÁBRICO', '200']
    ['4', 'AVENIDA DE LIBIA', '200']
    ['5', 'JARDINES DE LA AGRICULTURA', '300']
    ['6', 'PLAN PARCIAL O7 PARCELA 12 B', '400']
    ['7', 'IGLESIA DE LA TRINIDAD', '300']
    ['8', 'CALLE DON LOPE DE LOS RÍOS 24', '100']
    ['9', 'CALLE FUENTE DE LOS PICADORES 4', '300']
    ['10', 'CALLE JOSE MARÍA VALDENEBRO 35 Y PREVISIÓN 24', '500']
    ['11', 'CALLE MORISCOS 28', '100']
    ['12', 'CALLE JULIO VALDELOMAR ESQUINA CALLE ANTÓN MONTORO', '600']
    ['13', 'AVENIDA DE AMÉRICA 5', '100']
    ['14', 'CALLE RONDA DE MARRUBIAL ESQUINA AGRUPACIÓN DE CÓRDOBA', '600']
    ['15', 'CABALLERIZAS REALES', '300']
    ['16', 'POLIGONO INDUSTRIAL LAS QUEMADAS', '200']
    ['17', 'AVENIDA DE LAS OLLERÍAS', '200']
    ['18', 'CALLE MARÍA CRISTINA 4', '100']
    ['19', 'CALLE PINTOR MARIANO BELMONTE 5', '100']
    ['20', 'CALLE CERRO 3', '100']

Una vez cargados los datos haremos correr el script para que nos busque las coordenadas. Usaremos el servicio de Google al que le hemos añadido el nombre de la ciudad, a comunidad autónoma y el país para limitar más la búsqueda.

Hay una cuestión que tenemos que tener en cuenta. **Cada servicio tiene sus propias condiciones y restricciones de uso**. En algunos casos como Google, Bing o Yahoo se necesita obtener una clave (API Key) para poder usarlo completamente. En otras ocasiones, si no es necesario dicha clave en un principio, podremos usar el servicio con ciertas limitaciones respecto al tiempo y número de accesos. Este último es el caso del servicio de Google que vamos a manejar en el ejemplo. Estas restricciones pueden provocar diferencias de resultados en la misma consulta. El caso de Nominatim de OpenStreetMap es diferente. Es un servicio gratuíto pero lamentablemente deja mucho que desear a nivel de dirección postal según la ciudad.

```python
with open('csv_in.csv', encoding="utf8") as csv_file:
    csv_data = csv.reader(csv_file, delimiter=',', quotechar='\'')
    for row in csv_data:
        print(row[0], row[1], row[2])
        geodir = geocoder.google('{}, Córdoba, Andalucía, Spain'.format(row[1]))
        print('Coordenadas: {}'.format(geodir.latlng))
```

    id direccion tipo
    Coordenadas: [37.889395, -4.776749199999999]
    1 CALLE RONQUILLO BRICEÑO 10 100
    Coordenadas: [37.881442, -4.7696885]
    2 CALLEJA DEL POSADERO 21 100
    Coordenadas: None:
    3 AVENIDA DEL MEDITERRÁNEO Y CALLE CANTÁBRICO 200
    Coordenadas: None
    4 AVENIDA DE LIBIA 200
    Coordenadas: [37.8913159, -4.7571579]
    5 JARDINES DE LA AGRICULTURA 300
    Coordenadas: [37.8876884, -4.7856429]
    6 PLAN PARCIAL O7 PARCELA 12 B 400
    Coordenadas: [37.8881751, -4.7793835]
    7 IGLESIA DE LA TRINIDAD 300
    Coordenadas: None
    8 CALLE DON LOPE DE LOS RÍOS 24 100
    Coordenadas: [37.8980935, -4.7769355]
    ...
    
Para terminar y ahorrarnos un paso en el trabajo SIG posterior vamos a crear un archivo de tipo **geojson** con los resultados para lo cual necesitaremos usar la librería JSON. Creamos la estructura del archivo geográfico y vamos añadiendo la información de las coordenadas y los datos auxiliares id y tipo. 

Para los registros no localizados también vamos generar un informe en formato texto que los almacene. En consola hemos añadido un pequeño contador de los resultados

El código Python final sería el siguiente.

```python
import csv
import json

import geocoder

geojson = {
    'type': 'FeatureCollection',
    'features': []
}
report_noloc = ''
results = 0
total = 0

with open('csv_in.csv', encoding="utf8") as csv_file:
    csv_data = csv.reader(csv_file, delimiter=',', quotechar='\'')
    next(csv_data) # skip header

    for row in csv_data:
        geodir = geocoder.google('{}, Córdoba, Andalucía, España'.format(row[1]))
        total += 1
        if geodir:
            print('{},{},{},{},{}'.format(
                int(row[0]), row[1], row[2], geodir.latlng[1], geodir.latlng[0]))
            geojson['features'].append({
                'type': 'Feature',
                'geometry': {
                    'type': 'Point',
                    'coordinates': [geodir.latlng[1], geodir.latlng[0]],
                },
                "properties": {
                    "id": row[0],
                    "direccion": row[1],
                    "tipo": row[2],
                }
            })
            results += 1
        else:
            print('{},{},{},0,0'.format(int(row[0]), row[1], row[2]))
            report_noloc += '{},{},{}\n'.format(int(row[0]), row[1], row[2])

    print('\nNumber of matches {}/{}'.format(results, total))

with open('geo_results.geojson', 'w') as geofile:
    geofile.write(json.dumps(geojson, indent=2))

with open('report.txt', 'w') as report_file:
    report_file.write('Number of matches {}/{}\n\n'.format(results, total))
    report_file.write(report_noloc)
```

    1,CALLE RONQUILLO BRICEÑO 10,100,-4.7696885,37.881442
    2,CALLEJA DEL POSADERO 21,100,-4.7717183,37.8813662
    3,AVENIDA DEL MEDITERRÁNEO Y CALLE CANTÁBRICO,200,-4.8016214,37.8932353
    4,AVENIDA DE LIBIA,200,0,0
    5,JARDINES DE LA AGRICULTURA,300,-4.7856429,37.8876884
    6,PLAN PARCIAL O7 PARCELA 12 B,400,-4.7793835,37.8881751
    7,IGLESIA DE LA TRINIDAD,300,-4.7832253,37.8825864
    8,CALLE DON LOPE DE LOS RÍOS 24,100,-4.7769355,37.8980935
    9,CALLE FUENTE DE LOS PICADORES 4,300,-4.785800399999999,37.8959443
    10,CALLE JOSE MARÍA VALDENEBRO 35 Y PREVISIÓN 24,500,-4.7916745,37.8792955
    11,CALLE MORISCOS 28,100,-4.773073999999999,37.8905922
    12,CALLE JULIO VALDELOMAR ESQUINA CALLE ANTÓN MONTORO,600,-4.7672471,37.8870909
    13,AVENIDA DE AMÉRICA 5,100,-4.7819829,37.8907273
    14,CALLE RONDA DE MARRUBIAL ESQUINA AGRUPACIÓN DE CÓRDOBA,600,-4.7689894,37.8933605
    15,CABALLERIZAS REALES,300,0,0
    16,POLIGONO INDUSTRIAL LAS QUEMADAS,200,-4.7235637,37.9021637
    17,AVENIDA DE LAS OLLERÍAS,200,-4.773498,37.892047
    18,CALLE MARÍA CRISTINA 4,100,-4.7771383,37.8850085
    19,CALLE PINTOR MARIANO BELMONTE 5,100,-4.7853749,37.8927635
    20,CALLE CERRO 3,100,-4.767593499999999,37.8861559
    Number of matches 18/20
    
Podemos ver el resultado en la aplicación [geojson.io](http://geojson.io/)

![Datos en geojson.io](/images/blog/201808_geocoder/geojsonio.PNG)

## Nota final

He querido mostrar a partir de un ejemplo sencillo las posibilidades que ofrece el usos de lenguajes como Python para trabajos geográficos de este tipo. Son utilidades que sin duda pueden ayudar a mejorar desde el punto de vista territorial la información disponible en una organización. 

Un geosaludo
