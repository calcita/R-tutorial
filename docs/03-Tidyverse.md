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
reviews <- readr::read_csv(url("http://data.insideairbnb.com/germany/be/berlin/2019-07-11/visualisations/reviews.csv"))
```

```
## Parsed with column specification:
## cols(
##   listing_id = col_double(),
##   date = col_date(format = "")
## )
```

```r
neighbour <- readr::read_csv(url("http://data.insideairbnb.com/germany/be/berlin/2019-07-11/visualisations/neighbourhoods.csv"))
```

```
## Parsed with column specification:
## cols(
##   neighbourhood_group = col_character(),
##   neighbourhood = col_character()
## )
```

```r
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



<!-- --- -->
<!-- # st_read() -->

<!-- - Los objetos sf tienen una clase que combina **'data.frame'** y **'sf'**  -->
<!-- <br><br> -->
<!-- -- -->

<!-- - Los objetos sf también tienen una columna especial que contiene los datos de geometría, usualmente llamado 'geom' o **'geometry'**. -->
<!-- <br><br> -->
<!-- -- -->

<!-- - Las funciones del paquete **dplyr** se pueden aplicar. Para saber la totalidad de funciones que son aplicables a un objeto de **clase 'sf'** consultar **methods()**. -->
<!-- <br><br> -->
<!-- -- -->

<!-- - Para la unión de objetos espaciales se usa **st_join(x, y)**. El método de join utilizado es siempre left join, manteniendo los registros del primer atributo. -->

<!-- --- -->
<!-- # Importar shapes -->

<!-- ```{r } -->
<!-- # cargo paquete -->
<!-- library(sf) -->

<!-- # importo shapes -->
<!-- barrios = st_read("shapes/GISPORTAL_GISOWNER01_BERLIN_BEZIRKE_BOROUGHS01.shp",stringsAsFactors = FALSE) -->

<!-- # consulto clase -->
<!-- class(barrios) -->

<!-- ``` -->
<!-- ```{r eval=FALSE} -->
<!-- # consulto métodos -->
<!-- methods(class = "sf")  -->
<!-- ``` -->


<!-- --- -->
<!-- # Mapa de coropletas -->

<!-- - [Buenas prácticas](https://blog.datawrapper.de/choroplethmaps/)  -->
<!-- <br><br> -->
<!-- -- -->

<!-- - Es un **mapa temático** en el que las regiones se colorean de un motivo que muestra una **medida estadística**. -->
<!-- <br><br> -->
<!-- -- -->

<!-- ```{r} -->
<!-- # cargo datos -->
<!-- load("berlin.Rdata") -->
<!-- ``` -->

<!-- --- -->
<!-- # Encoding -->

<!-- ```{r } -->
<!-- library(stringi) -->
<!-- ``` -->
<!-- ```{r eval=FALSE} -->
<!-- # con qué encoding vienen los datos?  -->
<!-- stri_enc_mark(barrios$BezName) -->
<!-- ``` -->
<!-- ```{r } -->
<!-- library(dplyr) -->
<!-- # defino que los lea como 'ISO-8859-1' y pase a 'UTF-8' -->
<!-- barrios <- barrios %>%  -->
<!--            mutate(BezName = stri_conv(BezName, from = 'ISO-8859-1', to = 'UTF-8', to_raw = FALSE)) -->
<!-- head(barrios$BezName,12) -->
<!-- ``` -->

<!-- --- -->
<!-- # Expresiones regulares -->

<!-- ```{r} -->
<!-- # los barrios están escritos igual? -->
<!-- table(unique(berlin$neighbourhood_group) %in% barrios$BezName) -->

<!-- # busco la expresión y reemplazo -->
<!-- library(stringr) -->
<!-- large <- barrios$BezName -->
<!-- small <- berlin$neighbourhood_group -->

<!-- berlin <- berlin %>% mutate(neighbourhood_group = stri_replace(str = small,regex = small, replacement = large , mode="all")) -->

<!-- # chequeo -->
<!-- table(unique(berlin$neighbourhood_group) %in% barrios$BezName) -->
<!-- ``` -->

<!-- --- -->
<!-- # ggplot2 -->
<!-- ```{r} -->
<!-- # cuento la cantidad de alojamientos por barrios -->
<!-- bn <- berlin %>% -->
<!--   group_by(neighbourhood_group) %>%  -->
<!--   summarise(median_price = median(price)) -->

<!-- # uno berlin con el objeto espacial barrios -->
<!-- bn <- left_join(bn, barrios, by = c("neighbourhood_group"="BezName")) -->

<!-- # calculo centroides de los polígonos -->
<!-- latlong_mean <-  barrios %>% st_centroid(geometry) -->

<!-- # convierto la geometría en 2 vectores -->
<!-- latlong_mean <- st_coordinates(latlong_mean$geometry) -->
<!-- latlong_mean <- tibble(latlong_mean[,1], latlong_mean[,2]) -->
<!-- names(latlong_mean) <- c('lat', 'lon') -->
<!-- bn <- bind_cols(bn, latlong_mean)  -->

<!-- library(ggplot2) -->
<!-- mapa<- ggplot(bn) + -->
<!--        geom_sf(aes(fill = median_price)) + -->
<!--        geom_text(aes(x = lat, y = lon, label = neighbourhood_group),  size = 3, hjust = 0.5)+ -->
<!--       scale_fill_viridis_c("# Alojamientos", option = "D") + -->
<!--       ggtitle("Alojamientos Airbnb por barrios de Berlin") + -->
<!--       theme_void()  -->
<!-- ``` -->
<!-- --- -->
<!-- # ggplot2 -->

<!-- ```{r echo=FALSE} -->
<!-- mapa -->
<!-- ``` -->


<!-- --- -->
<!-- # leaflet -->

<!-- - El paquete leaflet es una extensión java script para R que permite hacer mapas interactivos. -->
<!-- <br><br> -->
<!-- -- -->

<!-- - [Tutorial](https://rstudio.github.io/leaflet/) para comenzar. -->
<!-- <br><br> -->
<!-- -- -->


<!-- --- -->
<!-- # leaflet() -->

<!-- | Función      | Descripción | -->
<!-- |---------------|:-------------:| -->
<!-- | leaflet()    |crea el objeto leaflet  |    -->
<!-- | addTiles() |  define el mapa de base, por defecto utiliza OpenStreetMap. [Opciones](http://leaflet-extras.github.io/leaflet-providers/preview/) | -->
<!-- | setView() | define por centroide y zoom | -->
<!-- | addMarkers() | marcadores a partir de una capa espacial o de pares de coordenadas.| -->

<!-- El orden de los comandos es importante.  -->

<!-- --- -->
<!-- # leaflet -->

<!-- ```{r eval=FALSE} -->
<!-- library(leaflet) -->

<!-- mapa <- leaflet() %>% -->
<!--         addTiles() %>%  -->
<!--         addMarkers(lng = -56.159158, lat = -34.888494,  -->
<!--                    popup ="UCU") -->
<!-- mapa -->
<!-- ``` -->


<!-- --- -->
<!-- # Mapa -->

<!-- ```{r echo=FALSE} -->
<!-- library(leaflet) -->

<!-- mapa <- leaflet() %>% -->
<!--         addTiles() %>%  -->
<!--         addMarkers(lng = -56.159158, lat = -34.888494,  -->
<!--                    popup ="UCU") -->
<!-- mapa -->
<!-- ``` -->

<!-- --- -->
<!-- # Alojamientos Berlin -->

<!-- ```{r eval=FALSE} -->
<!-- # Alojamientos caros de Airbnb en Berlin -->
<!-- top <- filter(berlin, price > 500 & !is.na(review_scores_rating)) -->

<!-- # de sf a sp -->
<!-- barrios.sp <- as(barrios, "Spatial") -->

<!-- barrios.sp@data <- merge(barrios.sp@data, top, by.x ="BezName" , by.y="neighbourhood_group") -->

<!-- library(leaflet) -->
<!-- airbnb = makeIcon("/home/calcita/MEGA/R/JOBS/UCU/Clases/programming-in-r/Slides/img/airbnb.png","/home/calcita/MEGA/R/JOBS/UCU/Clases/programming-in-r/Slides/img/airbnb@2x.png", 18, -->
<!--            18)  -->

<!-- mapa <- leaflet(data = barrios.sp) %>% -->
<!--         #setView() -->
<!--         addTiles() %>% -->
<!--         addMarkers(lng = ~longitude, lat = ~latitude, icon = airbnb)   -->
<!--         #addCircles()  -->
<!--         #addLegend() -->
<!-- mapa      -->
<!-- ``` -->

<!-- --- -->
<!-- # Alojamientos Berlin -->

<!-- ```{r echo=FALSE} -->
<!-- # Alojamientos caros de Airbnb en Berlin -->
<!-- top <- filter(berlin, price > 500 & !is.na(review_scores_rating)) -->

<!-- # de sf a sp -->
<!-- barrios.sp <- as(barrios, "Spatial") -->

<!-- barrios.sp@data <- merge(barrios.sp@data, top, by.x ="BezName" , by.y="neighbourhood_group") -->

<!-- library(leaflet) -->
<!-- airbnb = makeIcon("/home/calcita/MEGA/R/JOBS/UCU/Clases/programming-in-r/Slides/img/airbnb.png","/home/calcita/MEGA/R/JOBS/UCU/Clases/programming-in-r/Slides/img/airbnb@2x.png", 18, -->
<!--            18)  -->

<!-- mapa <- leaflet(data = barrios.sp) %>% -->
<!--         #setView() -->
<!--         addTiles() %>% -->
<!--         addMarkers(lng = ~longitude, lat = ~latitude, icon = airbnb)   -->
<!--         #addCircles()  -->
<!--         #addLegend() -->
<!-- mapa     -->
<!-- ``` -->

