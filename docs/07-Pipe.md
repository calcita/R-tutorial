# Pipe: **%>%**

El **‘pipe’** -por su nombre en inglés- estructura una secuencia de operaciones sobre los datos de izquierda a derecha.

A diferencia de la anidación de funciones que implica operaciones de adentro para afuera. 

En lugar de f(x): x %>% f()

![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/pipe-shortcut.png)

## ¿Cómo sería preparar un mate en R?

<iframe src="https://giphy.com/embed/2x0UnZn4CNObIedrqG" width="600" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/emoji-mate-emojidelmate-2x0UnZn4CNObIedrqG"></a></p>


## %>% 

**¿Preparar el mate con o sin 'pipe'?**


![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/icons8-mate-96.png)

<br><br><br><br>
![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/icons8-mate-100.png)






```r
# Mate con 'pipe'

mate %>% 
        poner_yerba() %>%
        hinchar() %>%
        colocar_bombilla() %>%
        cebar()
```
<br><br>


```r
# Mate sin 'pipe'

cebar(colocar_bombilla(hinchar(poner_yerba(mate))))
```



<br><br>
¿Cuál código te parece más claro?
<!-- --- -->
<!-- # Equivalencias -->

<!-- ![](https://raw.githubusercontent.com/calcita/Curso-rECH/master/images/equivalencias.png) -->

<!-- Y hay otros varios operadores útiles de la librería [magrittr](https://github.com/tidyverse/magrittr/blob/master/vignettes/magrittr.Rmd) -->


<!-- # %<>% -->

<!-- - La librería `magrittr` trae también entre sus funciones y operadores, un pipe de asignación. -->
<!-- <br><br> -->
<!-- -- -->

<!-- - Con el operador `%<>%` además de conectar nuestro objeto con las funciones subsiguientes, sobreescribe con el resultado de todo el proceso el objeto inicial. -->
<!-- -- -->

<!-- ```{r eval=FALSE} -->
<!-- h2018 <- h2018 %>% filter(dpto == 1) -->

<!-- ``` -->
<!-- -- -->

<!-- Es lo mismo que... -->
<!-- ```{r} -->

<!-- library(magrittr) -->

<!-- h2018 %<>% filter(dpto == 1) -->
<!-- ``` -->


<!-- --- -->
<!-- # <!--html_preserve--><i class="fas  fa-user-friends " style="color:#fc9272;"></i><!--/html_preserve-->  dplyr::group_by() -->

<!-- ```{r eval=FALSE} -->
<!-- h2018_sub %>% -->
<!--   group_by(region_3) %>% -->
<!--   summarise(promedio_y = mean(ht11)) -->
<!-- ``` -->


<!-- Sin el pipe teníamos: -->

<!-- ```{r eval=FALSE} -->
<!-- # promedio de ingresos por cada Región -->

<!-- summarise(group_by(h2018, region_3), promedio = mean(ht11)) -->
<!-- ``` -->

<!-- --- -->
<!-- # <!--html_preserve--><i class="fas  fa-user-friends " style="color:#fc9272;"></i><!--/html_preserve-->  dplyr::ungroup() -->

<!-- La función `ungroup()` te permitirá desagrupar para volver agrupar por otra variable dentro de la misma concatenación de acciones. -->

<!-- ```{r eval=FALSE} -->
<!-- h2018_sub %>% -->
<!--   group_by(region_3) %>% -->
<!--   mutate(media_y_region = mean(ht11)) %>% -->
<!--   ungroup() %>% -->
<!--   group_by(dpto) %>% -->
<!--   mutate(media_y_dpto = mean(ht11)) -->

<!-- ``` -->

