# Paquetes

La instalación de un paquete se realiza una única vez en la computadora. Para poder usar un paquete en determinada sesión de R, es necesario cargarlo cada vez que se abre Rstudio.

* Para instalar un paquete desde el repositorio oficial 


```r
# instalamos el paquete 'readr' desde el repositorio CRAN
# se hace una única vez
install.packages("readr") 
```
		
* Para instalar un paquete desde github


```r
# instalamos el paquete 'readr' alojado en github
# es del usuario hadley (Hadley Wickham). 
devtools::install.github("/hadley/readr") 
```

* Para que quede disponible debemos cargarlo en cada sesión


```r
library(readr) 
```
