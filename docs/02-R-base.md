

<!-- Now let's talk details. -->

<!-- xfun -->

<!-- https://cran.r-project.org/web/packages/xfun/vignettes/xfun.html -->

# R Base

<!--html_preserve--><script>
  addClassKlippyTo("pre.r, pre.markdown");
  addKlippy('left', 'top', 'auto', '1', 'Click to copy', 'Done');
</script><!--/html_preserve-->



<center>
![](https://live.staticflickr.com/4682/39063699342_e9159bc269_c_d.jpg)
</center>

Base R refiere a la colección de funciones que vienen por defecto cuando instalamos R y queda disponibles para usar cada vez que abrimos el programa. Podemos decir que esas fuciones son las que contiene el paquete Base. El resto de las funciones vienen en paquetes que debemos instalar y luego en cada nueva sesión, cargarlos.

# Objetos

R es un programa **'orientado a objetos'**: variables, datos, funciones, resultados, etc., se guardan en la memoria RAM en forma de objetos con un nombre específico sin usar archivos temporales. 

Cada clase de objeto tiene diferentes atributos que determinan la forma en que trabajan dentro de R, es decir, define cuáles funciones se le pueden aplicar. 

Estos objetos se pueden modificar o manipular con **operadores** y **funciones** --que a su vez son objetos--. 

Bajo este término se esconde la simplicidad y flexibilidad de R. 

Algunas de las clases más comunes de objetos son: 'integer', 'numeric', 'character', 'logical' (son vectores), 'matrix', 'data.frame', 'list' y 'function'.


## Tipo de objetos

La cantidad de clases de objetos es muy grande y crece permanentemente a medida que se crean nuevos paquetes.


| Objeto      | Dimensión o largo           | Tipo de elementos | Ejemplo
|---------------|:-------------:|:------:|:------:|
| Vector    | length() | similares |<!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--> |
| Matriz   | dim() | similares |   <!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--><!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--> |
| Marco de datos    | dim() | diferentes |<!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--><!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:blue;"></i><!--/html_preserve--> <!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:green;"></i><!--/html_preserve-->|
| Lista   | length() | diferentes |<!--html_preserve--><i class="fas  fa-circle " style="color:red;"></i><!--/html_preserve--> <br> <!--html_preserve--><i class="fas  fa-circle " style="color:blue;"></i><!--/html_preserve--> <br> <!--html_preserve--><i class="fas  fa-circle " style="color:green;"></i><!--/html_preserve-->| 

## Vectores 

![](images/vector.png){ width=15% } 

Un vector es una <span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >colección de uno o más objetos del mismo tipo</span> (números o caracteres pero no ambos). Un escalar también es un vector en R.


### c()

- Crea un vector

- Según sus elementos será la clase del vector: *character*, *numeric*, *integer*, *logical*

- Cada elemento va separado por una coma

- Con la función **class()** compruebo que tipo de objeto es


## Vector


```r
x <- c(15, 16, 17, 19)
x
```

```
## [1] 15 16 17 19
```

```r
class(x)
```

```
## [1] "numeric"
```


```r
y <- x / 2
y
```

```
## [1] 7.5 8.0 8.5 9.5
```

```r
class(y) # numeric porque contiene decimales
```

```
## [1] "numeric"
```


## Vector

Para el caso de "palabras" ("strings"), la clase "character" es la que utiliza R para manejar este tipo de objetos. Al igual que en la mayoría de los lenguajes de programación, R utiliza las comillas dobles (") o simples (') para delimitar un string. 

<!-- # Nótese que al usar las comillas se puede incluir cualquier caracter dentro,  -->
<!-- # sin tener que preocuparse de que R lo interprete como un comando. Es decir,  -->
<!-- # se toma lo que está entre comillas de forma literal, razón por la cual  -->
<!-- # estos tipos de objetos son llamados "strings literals" muchas veces. -->


```r
w <- c("15", "16", "17", "19")
w
```

```
## [1] "15" "16" "17" "19"
```

```r
class(w)
```

```
## [1] "character"
```


```r
w <- c("lunes", "martes", "miércoles", "viernes")
w
```

```
## [1] "lunes"     "martes"    "miércoles" "viernes"
```

```r
class(w)
```

```
## [1] "character"
```


## Ejemplo vectores

Comparemos algunas características de R con otros software estadísticos como Stata y SPSS.
Esta tabla la tomé de [Princeton University](https://imgv2-2-f.scribdassets.com/img/document/353774131/original/365bf63409/1573401036?v=1), la traduje y le agregué el año de creación.

|Características | R | SPSS | Stata |
|-----------------|-------|----------|----------------|
| Año | 1993| 1968 | 1985|
| Curva aprendizaje | Muy empinada | Plana  | Empinada |
| Interfaz| Programación| Point and click | Programación/Point and click |
| Manipulación de datos| Avanzada | Moderada | Avanzada |
| Análisis de datos| Potente/Versátil | Potente | Potente|
| Gráficos| Excelentes|Muy buenos | Muy buenos |
|Software libre| 1| 0| 0 |
|Costo| Gratuito| Muy costoso| Accesible |


```r
anio <- c(1993, 1968, 1985)
software_libre <- c(T, F, F)
costo <- c("gratuito", "costoso", "accesible")
```


```r
length(anio)
```

```
## [1] 3
```

```r
class(anio)
```

```
## [1] "numeric"
```

## Coerción

Como mencionamos anteriormente, estos elementos deben ser todos de la misma clase. Si se combinan objetos de diferente clase, R reasigna los elementos a la clase apropiada. Si contiene números y texto el vector será de clase `character`.

La coerción es necesaria para el funcionamiento correcto de R. Al mismo tiempo puede ser una fuente de errores si no se tiene en cuenta.

Un texto sin comillas en R es un objeto (siempre que cumpla las reglas de un nombre de objeto).


## Vectorización

R vectoriza las operaciones de manera que si sumo un número a un vector numérico, a cada elemento del vector le sumará ese número. Esta propiedad es una ventaja ya que permite evitar loops en muchas de situaciones y de esta manera se obtiene un código más 'limpio' y eficiente.


```r
x <- -1:4 
x
```

```
## [1] -1  0  1  2  3  4
```

El operador  <span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >:</span> sirve para generar vectores numéricos


```r
x + 5 # adiciono 5 
```

```
## [1] 4 5 6 7 8 9
```


```r
x * 3 # multiplico por 3 
```

```
## [1] -3  0  3  6  9 12
```

## Funciones descriptivas de un vector numérico

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >length(x)</span>: devuelve la cantidad de elementos de x

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >sort(x, decreasing = F)</span>: ordena los elementos de manera creciente 

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >sum(x)</span>: devuelve la suma de los elementos de x

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >max(x)</span>: máximo

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >min(x)</span>: mínimo

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >mean(x)</span>: promedio aritmético de x

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >median(x)</span>: mediana de x

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >sd(x)</span>: desvío estándar de x

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >var(x)</span>: varianza de x

<span style="     border-radius: 4px; padding-right: 4px; padding-left: 4px; background-color: #b3e2cd !important;" >summary(x)</span>: resumen descriptivo de x (mínimo, máximo, media, mediana, cuartiles)

## Data frame

![](images/dataframe.png){ width=15% } 

- Puede verse como un conjunto de vectores de diferente tipo pero de igual largo.


```{.r .klippy}
# vector numeric
anio <- c(1993, 1968, 1985)

# vector lógico

software_libre <- c(T, F, F)

# vector character
costo <- c("gratuito", "costoso", "accesible")


# data frame
df <- data.frame(anio, software_libre, costo)
class(df)
```

```
## [1] "data.frame"
```


```r
knitr::kable(df)
```

<table>
 <thead>
  <tr>
   <th style="text-align:right;"> anio </th>
   <th style="text-align:left;"> software_libre </th>
   <th style="text-align:left;"> costo </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 1993 </td>
   <td style="text-align:left;"> TRUE </td>
   <td style="text-align:left;"> gratuito </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1968 </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> costoso </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1985 </td>
   <td style="text-align:left;"> FALSE </td>
   <td style="text-align:left;"> accesible </td>
  </tr>
</tbody>
</table>

- En un conjunto de datos, cada variable/columna es un vector. 


```r
class(df$anio); class(df$software_libre); class(df$costo)
```

```
## [1] "numeric"
```

```
## [1] "logical"
```

```
## [1] "factor"
```

- En general el data frame vendrá dado en un archivo.

## Explorar los datos


```r
# dimensiones del objeto
dim()
```

```r
# nombres de variables
names()

# estructura del objeto
str()

# resumen descriptivo de variables
summary()
```

## Guardar objeto en formato RData


```r
save(df, file = "data/df.RData") 
```

El primer elemento debe ser un **objeto**. Podrían ser más de uno.

Es necesario nombrar el argumento **'file'** definiendo ruta y nombre de archivo.

Si en **file** solo se define el nombre del archivo, se guarda en el directorio de trabajo actual: **getwd()**

El **nombre** del objeto y el archivo pueden coincidir, pero no necesariamente.

Un archivo Rdata es más **liviano** que cualquier otro formato externo.
