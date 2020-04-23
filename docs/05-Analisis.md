# Análisis de datos

<center>
![Barcelona](images/barcelona/201706_Barcelona_088_lnz.jpg)
</center>

Ejemplificaremos con datos de alojamientos de Airbnb en la ciudad de Barcelona, España, disponibles en [Inside Airbnb](http://data.insideairbnb.com). La elección de los datos no responde a hacerle publicidad a esta empresa, simplemente los elegí porque contiene variables interesantes.

<!-- http://data.insideairbnb.com/spain/catalonia/barcelona/2020-02-16/visualisations/neighbourhoods.geojson -->

Accedemos a los datos desde la url o de manera local si ya los descargamos en la computadora. Está disponible el listado de alojamientos con sus características en un archivo csv y la información geográfica de los barrios en un formato geojson. Primero trabajaremos con el listado de alojamientos.


```r
ruta <- "http://data.insideairbnb.com/spain/catalonia/barcelona/2020-02-16/visualisations/listings.csv"
```


```r
datos <- read.csv(ruta)
```



```r
datos <- readr::read_csv(ruta)
```

Pero si previamente los bajamos, podemos importarlos desde la carpeta data del proyecto


```r
datos <- readr::read_csv("data/listings.csv")
```
Lo primero que conviene hacer, sobre todo si no hemos trabajado antes con estos datos, es explorarlos. Las funciones básicas que dispone R para esto son las siguientes:

- head(): muestra los primeros casos. Por defecto, los primeros 6.
- tail(): muestra los últimos 6 casos. Por defecto, los últimos 6.
- View(): para mirar la base, como si abriéramos el archivo. Si es muy grande no se mostrarán todas filas ni todas las variables.
- summary(): brinda un resumen estadístico de cada variable cuando se aplica a un data.frame o de la variable en particular indicada. Si la variable es numérica se muestra el mínimo, máximo y los cuartiles. En caso de una variable de texto se muestra una tabla de los valores que toma. 
- names(): brinda el listado de nombres de variables.


```r
# primeros casos
head(datos)

# ver los datos
View(datos)

# resumen estadistico
summary(datos)

# nombres de variables
names(datos)
```

Acá puedes ver la descripción de las variables que contiene la base.

**Tabla de variables**

| Variable | Tipo | Descripción |
|----------|----------|-----------|
|id | identificador del alojamiento| numérica |
|name | nombre del alojamiento| texto |
|host_id | identificador de la persona anfitriona| numérica|
|host_name | nombre de la persona anfitriona | texto |
|neighbourhood_group | nombre del barrio agrupado | texto |
|neighbourhood | nombre del barrio|texto |
|latitude | latitud| numérica |
|longitud | longuitud| numérica |
|room_type | tipo de habitación| texto |
|price | precio| numérica |
|minimum_nights | cantidad mínima de noches| numérica |
|number_of_reviews |cantidad de evaluaciones | numérica |
|last_review | última evaluación| fecha |
|reviews_per_month | evaluaciones por mes| numérica |
|calculated_host_listings_count | | |
|availability_365 | disponibilidad en el  año | numérica |

Exploremos una variable character como lo es *room_type* y una numeric como *price*.


```r
ggplot(data = datos) + 
  geom_boxplot(
    mapping = aes(x = price)
  )
```


## Paquete dplyr

## Seleccionar filas

## Seleccionar columnas

## Renombrar variables

## Ordenar casos por cierta variable

## Modificar o crear una nueva variable

## Agrupar casos 

## Resumir los datos

## Operadores lógicos
