# Data

Ejemplificaremos con datos de alojamientos de Airbnb en la ciudad de Berlin, Alemania, disponibles en [Inside Airbnb](http://data.insideairbnb.com/germany/be/berlin/2019-07-11/data/listings.csv.gz)

Accedemos a los datos desde la url. 


```r
listings <- readr::read_csv(url("http://data.insideairbnb.com/germany/be/berlin/2019-07-11/visualisations/listings.csv"))
```

```
## Parsed with column specification:
## cols(
##   id = col_double(),
##   name = col_character(),
##   host_id = col_double(),
##   host_name = col_character(),
##   neighbourhood_group = col_character(),
##   neighbourhood = col_character(),
##   latitude = col_double(),
##   longitude = col_double(),
##   room_type = col_character(),
##   price = col_double(),
##   minimum_nights = col_double(),
##   number_of_reviews = col_double(),
##   last_review = col_date(format = ""),
##   reviews_per_month = col_double(),
##   calculated_host_listings_count = col_double(),
##   availability_365 = col_double()
## )
```

```r
ratings <- readr::read_csv("data/ratings.csv")
```

```
## Parsed with column specification:
## cols(
##   id = col_double(),
##   review_scores_rating = col_double()
## )
```

```r
# reviews <- readr::read_csv(url("http://data.insideairbnb.com/germany/be/berlin/2019-07-11/visualisations/reviews.csv"))
# 
# neighbour <- readr::read_csv(url("http://data.insideairbnb.com/germany/be/berlin/2019-07-11/visualisations/neighbourhoods.csv"))

# "http://data.insideairbnb.com/germany/be/berlin/2019-07-11/visualisations/neighbourhoods.geojson"
```

## GDS

- R no es un SIG (Sistemas de Información Geográficos)

- R permite hacer Ciencia de Datos Geográficos (SDG)

| Atributos     | SIG | SDG |
|---------------|:-------------:|:-------------:|
|Disciplinas | Geografía | Geografía, Computación, Estadística|
| Foco | Interfaz Gráfica | Código |
| Reproducibilidad | Mínimo | Máximo |


## Paquetes

- sp, sf: para manejar información espacial vectorial
- raster: para trabajar con rasters

- ggplot2, rasterVis, tmap, leaflet, o mapview: para visualizar información espacial

- Es sencillo conectar R con programas SIG: GRASS GIS (rgrass7), SAGA (RSAGA), QGIS (RQGIS y qgisremote), incluso ArcGIS (arcgisbinding).

## sf 

Combina las funcionalidades de 3 paquetes: **sp**, **rgeos** y **rgdal**

Ventajas respecto a otros paquetes: 

Mayor **velocidad** para importar y exportar los datos

Más tipos de **geometrías** soportadas

**Compatibilidad** con tidyverse. Funciona el pipe!

El paquete **sp** es predecesor de sf.

Muchos paquetes espaciales de R todavía dependen del paquete sp, por lo tanto, es importante saber cómo **convertir**.

Convertir objetos  **sf** a **sp**


```r
# Para transformar de SF a SP
objeto.sp <- as(objeto.sf, "Spatial")
```

Convertir objetos  **sp** a **sf**


```r
# Para transformar de SP a SF
objeto.sf <- st_as_sf(objeto.sp)
```



## st_read()

Los objetos sf tienen una clase que combina **'data.frame'** y **'sf'**

Los objetos sf también tienen una columna especial que contiene los datos de geometría, usualmente llamado 'geom' o **'geometry'**.

Las funciones del paquete **dplyr** se pueden aplicar. Para saber la totalidad de funciones que son aplicables a un objeto de **clase 'sf'** consultar **methods()**.

Para la unión de objetos espaciales se usa **st_join(x, y)**. El método de join utilizado es siempre left join, manteniendo los registros del primer atributo.

## Importar shapes

Los shapes con límites de los barrios de Berlin los obtenemos [aquí](http://geoserver01.uit.tufts.edu/wfs?outputformat=SHAPE-ZIP&request=GetFeature&service=wfs&srsName=EPSG%3A4326&typeName=sde%3AGISPORTAL.GISOWNER01.BERLIN_BEZIRKE_BOROUGHS01&version=2.0.0).

Para trabajar descomprimimos el zip y dejamos los 5 archivos en una misma carpeta.


```r
# cargo paquete
library(sf)
```

```
## Linking to GEOS 3.5.1, GDAL 2.2.2, PROJ 4.9.2
```

```r
# importo shapes
unzip("data/GISPORTAL_GISOWNER01_BERLIN_BEZIRKE_BOROUGHS01.zip", exdir = "data/") 
barrios <- st_read("data/GISPORTAL_GISOWNER01_BERLIN_BEZIRKE_BOROUGHS01.shp", stringsAsFactors = FALSE)
```

```
## Reading layer `GISPORTAL_GISOWNER01_BERLIN_BEZIRKE_BOROUGHS01' from data source `/home/calcita/MEGA/R/github.io/R-tutorial/R-tutorial/data/GISPORTAL_GISOWNER01_BERLIN_BEZIRKE_BOROUGHS01.shp' using driver `ESRI Shapefile'
## Simple feature collection with 12 features and 3 fields
## geometry type:  MULTIPOLYGON
## dimension:      XY
## bbox:           xmin: 13.08835 ymin: 52.33824 xmax: 13.76114 ymax: 52.67551
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```

```r
# consulto clase 
class(barrios)
```

```
## [1] "sf"         "data.frame"
```

```r
# consulto métodos
methods(class = "sf")
```


## Mapa de coropletas

- [Buenas prácticas](https://blog.datawrapper.de/choroplethmaps/)

- Es un **mapa temático** en el que las regiones se colorean de un motivo que muestra una **medida estadística**.


## Encoding


```r
library(stringi)
```

```r
# con qué encoding vienen los datos?
stri_enc_mark(barrios$BezName)
```

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
# defino que los lea como 'ISO-8859-1' y pase a 'UTF-8'
barrios <- barrios %>%
           mutate(BezName = stri_conv(BezName, from = 'ISO-8859-1', to = 'UTF-8', to_raw = FALSE))
head(barrios$BezName,12)
```

```
##  [1] "Mitte"                      "Friedrichshain-Kreuzberg"  
##  [3] "Pankow"                     "Charlottenburg-Wilmersdorf"
##  [5] "Spandau"                    "Steglitz-Zehlendorf"       
##  [7] "Tempelhof-Schöneberg"       "Neukölln"                  
##  [9] "Treptow-Köpenick"           "Marzahn-Hellersdorf"       
## [11] "Lichtenberg"                "Reinickendorf"
```


## Expresiones regulares


```r
# los barrios están escritos igual?
table(unique(listings$neighbourhood_group) %in% barrios$BezName)
```

```
## 
## FALSE  TRUE 
##     5     7
```

```r
# busco la expresión y reemplazo
library(stringr)
large <- barrios$BezName
small <- listings$neighbourhood_group

berlin <- listings %>% mutate(neighbourhood_group = stri_replace(str = small,regex = small, replacement = large , mode="all"))
```

```
## Warning in stri_replace_all_regex(str, regex, replacement, ...): longer
## object length is not a multiple of shorter object length
```

```r
# chequeo
table(unique(berlin$neighbourhood_group) %in% barrios$BezName)
```

```
## 
## TRUE 
##   12
```

Uno los data frame listings  y ratings para agregar la variable 'review_score'


```r
berlin <- left_join(berlin, ratings, by = "id")
```


## ggplot2

```r
# cuento la cantidad de alojamientos por barrios
bn <- berlin %>%
  group_by(neighbourhood_group) %>%
  summarise(median_price = median(price))

# uno berlin con el objeto espacial barrios
bn <- left_join(bn, barrios, by = c("neighbourhood_group"="BezName"))

# calculo centroides de los polígonos
latlong_mean <-  barrios %>% st_centroid(geometry)

# convierto la geometría en 2 vectores
latlong_mean <- st_coordinates(latlong_mean$geometry)
latlong_mean <- tibble(latlong_mean[,1], latlong_mean[,2])
names(latlong_mean) <- c('lat', 'lon')
bn <- bind_cols(bn, latlong_mean)

library(ggplot2)
mapa<- ggplot(bn) +
       geom_sf(aes(fill = median_price)) +
       geom_text(aes(x = lat, y = lon, label = neighbourhood_group),  size = 3, hjust = 0.5)+
      scale_fill_viridis_c("# Alojamientos", option = "D") +
      ggtitle("Alojamientos Airbnb por barrios de Berlin") +
      theme_void()
mapa
```

## leaflet

- El paquete leaflet es una extensión java script para R que permite hacer mapas interactivos.

- [Tutorial](https://rstudio.github.io/leaflet/) para comenzar.

## leaflet()

| Función      | Descripción |
|---------------|:---------------------------------------:|
| leaflet()    |crea el objeto leaflet  |
| addTiles() |  define el mapa de base, por defecto utiliza OpenStreetMap. [Opciones](http://leaflet-extras.github.io/leaflet-providers/preview/) |
| setView() | define por centroide y zoom |
| addMarkers() | marcadores a partir de una capa espacial o de pares de coordenadas.|

El orden de los comandos es importante.


## leaflet


```r
library(leaflet)

contenido <- paste(sep = "<br/>",
               paste0("<img src='https://upload.wikimedia.org/wikipedia/commons/4/45/Estadio_Centenario_%28vista_a%C3%A9rea%29.jpg", "' />"),
               paste0("<b>Name: </b>", "Estadio Centenario"),
               paste0("<b>Place: </b>", "Montevideo, Uruguay"),
               paste0("<a href='https://es.wikipedia.org/wiki/Estadio_Centenario", "'>Link</a>"))

mapa <- leaflet() %>%
        addTiles() %>%
        addMarkers(lng = -56.159158, lat = -34.888494,
                   popup = contenido)
mapa
```



## Mapa

<!--html_preserve--><div id="htmlwidget-a7d90e6ce3b6e311e4f8" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-a7d90e6ce3b6e311e4f8">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":1,"detectRetina":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap<\/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA<\/a>"}]},{"method":"addMarkers","args":[-34.89445,-56.15253,null,null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},"Estadio Centenario",null,null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"limits":{"lat":[-34.89445,-34.89445],"lng":[-56.15253,-56.15253]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


## Alojamientos Berlin


```r
# Alojamientos caros de Airbnb en Berlin
top <- filter(berlin, price > 500 & !is.na(review_scores_rating))

# de sf a sp
barrios.sp <- as(barrios, "Spatial")

barrios.sp@data <- merge(barrios.sp@data, top, by.x ="BezName" , by.y="neighbourhood_group")

library(leaflet)
airbnb = makeIcon("https://raw.githubusercontent.com/calcita/R-tutorial/master/images/airbnb.png","/https://raw.githubusercontent.com/calcita/R-tutorial/master/images/airbnb@2x.png", 18, 18)

mapa <- leaflet(data = barrios.sp) %>%
        #setView()
        addTiles() %>%
        addMarkers(lng = ~longitude, lat = ~latitude, icon = airbnb)
        #addCircles()
        #addLegend()
mapa
```


## Alojamientos Berlin

<!--html_preserve--><div id="htmlwidget-f0fe880e6a42e58a6579" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-f0fe880e6a42e58a6579">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":1,"detectRetina":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap<\/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA<\/a>"}]},{"method":"addMarkers","args":[[52.46973,52.54012,52.49941,52.50779,52.49349,52.53905,52.48998,52.50619,52.48922,52.51729,52.49798,52.5471,52.54283,52.50027,52.53235,52.50398,52.53064,52.49006,52.50267,52.5331,52.54067,52.54344,52.52187,52.53498,52.53952,52.50453,52.49851,52.54038,52.48878],[13.39235,13.42193,13.42529,13.4226,13.42049,13.40173,13.33085,13.37759,13.33131,13.4121,13.33444,13.37089,13.42292,13.45813,13.32715,13.48594,13.28734,13.33171,13.36451,13.32778,13.35579,13.4213,13.39967,13.43383,13.42362,13.41376,13.34073,13.42299,13.42196],{"iconUrl":{"data":"https://raw.githubusercontent.com/calcita/R-tutorial/master/images/airbnb.png","index":0},"iconRetinaUrl":{"data":"https://raw.githubusercontent.com/calcita/R-tutorial/master/images/airbnb@2x.png","index":0},"iconWidth":18,"iconHeight":18},null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},null,null,null,null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"limits":{"lat":[52.46973,52.5471],"lng":[13.28734,13.48594]}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

