# Tidyverse

tidyverse proporciona una forma unificada, armoniosa y más poderosa de trabajar con datos que la que ofrece el paquete base.

.center[
<img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/tidyverse.png" width="300px" />
]

## Paquetes 


<img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/readr.png" width="70px" /><img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/haven.png" width="70px" />

<img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/dplyr.png" width="70px" /><img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/tidyr.png" width="70px" />

<img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/stringr.png" width="70px" /><img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/labelled.png" width="70px" />

<img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/ggplot2.png" width="70px" /><img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/sf.gif" width="70px" />

<img src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/srvyr.png" width="70px" />


<br><br>
**[Importar archivos](https://github.com/rstudio/cheatsheets/raw/master/translations/spanish/data-import-cheatsheet_Spanish.pdf)**: csv, txt, dta, sav, etc.
<br><br><br>

**[Limpiar](https://github.com/rstudio/cheatsheets/raw/master/data-import.pdf) y [transformar](https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf)**
<br><br><br><br>

**Manipular [texto](https://github.com/rstudio/cheatsheets/raw/master/translations/spanish/strings_Spanish.pdf) y [etiquetas](http://larmarange.github.io/labelled/index.html)**
<br><br><br><br>

**Visualización: [gráficos](https://github.com/rstudio/cheatsheets/raw/master/translations/spanish/ggplot2.pdf) y [mapas](https://github.com/rstudio/cheatsheets/raw/master/sf.pdf)**
<br><br>

**Inferencia**: [**estimaciones**](http://gdfe.co/srvyr/) puntuales y por intervalo


## dplyr



La estructura de datos más importante en R es el **data frame**.

Permite representar la información en forma de tabla, donde cada **fila** representa una **observación** y cada **columna** represente una **variable**.

El paquete dplyr no provee ninguna funcionalidad que no pueda ser realizada con las funciones del paquete base, sin embargo, es más **simple** y **rápido** (está escrito en C++).


```r
# install.packages("dplyr")
library(dplyr)
```

<!-- - Todas las funciones del paquete tiene la particularidad de que su primer argumento es el data frame al que le realizará la operación, mientras que los subsiguiente argumentos describen como realizar tal operación. Finalmente el resultado de todas estas funciones es un nuevo data frame. -->


<!-- # dplyr::verbo() -->

<!-- ```{r out.width = "500px" ,fig.align="center", echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/dplyr_schema.png") -->
<!-- ``` -->

<!-- # <!--html_preserve--><i class="fas  fa-hand-pointer " style="color:#fc9272;"></i><!--/html_preserve--> dplyr::select() -->

<!-- Selecciona variables/columnas -->

<!-- ```{r eval =FALSE} -->
<!-- # selecciono las variables "dpto", "ht11", "secc" -->
<!-- h2018_sub <- select(h2018, dpto, region_3, ht11, secc, pobre06) -->
<!-- h2018_sub -->
<!-- ``` -->



<!-- # ![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/pizza.png) dplyr::slice() -->

<!-- Selecciona observaciones/filas según su posición -->

<!-- ```{r eval=FALSE} -->
<!-- # selecciono las filas 1 y 5 -->
<!-- slice(h2018_sub, 1, 5) -->
<!-- ``` -->

<!-- ```{r eval=FALSE} -->
<!-- # selecciono las filas de 1 a 5 -->
<!-- slice(h2018_sub, 1:5) -->
<!-- ``` -->


<!-- # <!--html_preserve--><i class="fas  fa-filter " style="color:#fc9272;"></i><!--/html_preserve--> dplyr::filter() -->

<!-- Selecciona observaciones/filas según una condición -->

<!-- ```{r eval=FALSE} -->
<!-- mvd <- filter(h2018_sub, dpto == 1) -->
<!-- mvd -->
<!-- ``` -->


<!-- ## Operadores -->

<!-- <!-- https://github.com/jumanbar/Curso-R/blob/master/lecciones/2.1a-operadores-relacionales-y-logicos.R --> -->

<!--  O lógico: **|** -->
<!-- ```{r eval=FALSE} -->
<!-- # selecciono los datos de Montevideo(1) y Canelones(3) -->
<!-- filter(h2018_sub, dpto == 1 | dpto == 3) -->
<!-- ``` -->

<!--  Y lógico: **&** -->
<!-- ```{r eval=FALSE} -->
<!-- # selecciono los datos de hogares de Montevideo(1) y que pertenezcan a la sección "01" -->
<!-- filter(h2018_sub, dpto == 1 & secc == "01") -->
<!-- ``` -->


<!--  No lógico: <!--html_preserve--><i class="fas  fa-exclamation "></i><!--/html_preserve--> -->
<!-- ```{r eval=FALSE} -->
<!-- # selecciono los hogares que no pertenezcan a la sección "01" -->
<!-- filter(h2018_sub, !secc == "01") -->
<!-- ``` -->
<!-- -- -->

<!--  inclusión: **%in%** -->
<!-- ```{r eval=FALSE} -->
<!-- # selecciono los datos en que el código de dpto esté incluido en el vector c(1,3,5) -->
<!-- filter(h2018_sub, dpto %in% c(1, 3, 5)) -->
<!-- ``` -->



<!-- # <!--html_preserve--><i class="fas  fa-sort " style="color:#fc9272;"></i><!--/html_preserve--> dplyr::arrange() -->

<!-- Ordena las observaciones según una variable -->
<!-- ```{r eval=FALSE} -->
<!-- arrange(h2018_sub, dpto) -->
<!-- ``` -->

<!-- Para ordenar de manera decreciente: -->
<!-- ```{r eval=FALSE} -->
<!-- arrange(h2018_sub, desc(dpto)) -->
<!-- ``` -->

<!-- Para ordenar por más de una variable: -->
<!-- ```{r eval=FALSE} -->
<!-- arrange(h2018_sub, desc(dpto), secc) -->
<!-- ``` -->

<!-- ```{r echo=FALSE} -->
<!-- head(arrange(h2018_sub,desc(dpto), secc)) -->
<!-- ``` -->


<!-- # <!--html_preserve--><i class="fas  fa-calculator " style="color:#fc9272;"></i><!--/html_preserve--> dplyr::top_n() -->



<!-- En el segundo caso el valor `0` iguala a 6 casos, y R devuelve todos los casos que impliquen empates para que el usuario decida como resolverlo.   -->


<!-- # <!--html_preserve--><i class="fas  fa-calculator " style="color:#fc9272;"></i><!--/html_preserve--> dplyr::summarise() -->

<!-- Calcula resumen de variables. -->

<!-- Se puede utilizar cualquier función que cumpla con que lo datos de entrada sean numéricos y como salida se entregue una constante. -->

<!-- Si la variable tiene datos faltantes se puede calcular el promedio sin considerarlos -->


<!-- # ![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/function.png) dplyr::mutate() -->

<!-- Crea nuevas variables -->


<!-- Es lo mismo que... -->


<!-- - Para categorizar lo no incluido en las clases se puede usar:  `TRUE ~` (Ver ?case_when) -->


<!-- # <!--html_preserve--><i class="fas  fa-table " style="color:#fc9272;"></i><!--/html_preserve--> dplyr::count() -->

<!-- Calcula una tabla de frecuencias -->


<!-- ## tally -->


<!-- # <!--html_preserve--><i class="fas  fa-user-friends " style="color:#fc9272;"></i><!--/html_preserve-->  dplyr::group_by() -->

<!-- - Permite hacer operaciones por grupos -->

<!-- - Anidar funciones vuelve confuso el código... -->

<!-- <img style="float: rigth;" src="https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/tool.png"> -->

<!-- # ![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/function.png) dplyr::n() -->

<!-- - Esta función se implementa específicamente para cada fuente de datos y sólo se puede utilizar desde dentro de `summarise()`, `mutate()` y `filter()`. -->


<!-- --- -->
<!-- # join (merge) data frames -->

<!-- .pull-left[ -->
<!-- ```{r out.width = "180px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/full_join.png") -->
<!-- ``` -->

<!-- ```{r out.width = "180px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/left_join.png") -->
<!-- ``` -->

<!-- ```{r out.width = "180px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/inner_join.png") -->
<!-- ``` -->


<!-- ] -->

<!-- .pull-rigth[ -->
<!-- <br> -->
<!-- ```{r out.width = "180px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/anti_join.png") -->
<!-- ``` -->

<!-- ```{r out.width = "180px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/rigth_join.png") -->
<!-- ``` -->

<!-- ```{r out.width = "180px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/semi_join.png") -->
<!-- ``` -->

<!-- ] -->

<!-- --- -->
<!-- # dplyr::full_join -->


<!-- ```{r out.width = "600px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://github.com/gadenbuie/tidyexplain/blob/master/images/full-join.gif?raw=true") -->
<!-- ``` -->


<!-- --- -->
<!-- # dplyr::semi_join() -->

<!-- ```{r out.width = "600px" ,echo=FALSE} -->
<!-- knitr::include_graphics("https://github.com/gadenbuie/tidyexplain/blob/master/images/semi-join.gif?raw=true") -->
<!-- ``` -->

<!-- --- -->
<!-- # Join base personas y hogares -->

<!-- Variable que identifica las observaciones en base hogares: 'numero' -->
<!-- Variable que identifica las observaciones en base personas: 'numero' e 'id' -->

<!-- ```{r eval = FALSE} -->
<!-- # importo base de personas -->
<!-- p2018 <- haven::read_sav("data/P_2018_Terceros.sav") -->
<!-- # reviso dimensiones -->
<!-- dim(p2018) -->
<!-- dim(h2018) -->

<!-- # fusiono las bases por la variable 'numero' -->
<!-- hp2018 <- left_join(h2018, p2018, by = "numero") -->
<!-- # reviso dimensiones -->
<!-- dim(hp2018) -->
<!-- ``` -->

