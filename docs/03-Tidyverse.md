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

