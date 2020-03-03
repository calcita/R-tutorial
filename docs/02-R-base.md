<!-- # R y Rstudio -->

<!-- ## Instalación  -->

<!-- ## Actualización de versiones -->

<!-- Now let's talk details. -->

<!-- xfun -->

<!-- https://cran.r-project.org/web/packages/xfun/vignettes/xfun.html -->

# Objetos

R es un programa **'orientado a objetos'**: variables, datos, funciones, resultados, etc., se guardan en la memoria RAM en forma de objetos con un nombre específico sin usar archivos temporales. 

Cada clase de objeto tiene diferentes atributos que determinan la forma en que trabajan dentro de R, es decir, define cuáles funciones se le pueden aplicar. 

Estos objetos se pueden modificar o manipular con **operadores** y **funciones** --que a su vez son objetos--. 

Bajo este término se esconde la simplicidad y flexibilidad de R. 

Algunas de las clases más comunes de objetos son: 'integer', 'numeric', 'character',
'logical' (son vectores), 'matrix', 'data.frame', 'list' y 'function'.


## Tipo de objetos

La cantidad de clases de objetos es muy grande y crece permanentemente a medida que se crean nuevos paquetes.


| Objeto      | Dimensión o largo           | Tipo de elementos | Ejemplo
|---------------|:-------------:|:------:|:------:|
| Vector    | length() | similares |<!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--> |
| Matriz   | dim() | similares |   <!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--><!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--> |
| Marco de datos    | dim() | diferentes |<!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:red;"></i><!--/html_preserve--><!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:blue;"></i><!--/html_preserve--> <!--html_preserve--><i class="fas  fa-ellipsis-v fa-3x " style="color:green;"></i><!--/html_preserve-->|
| Lista   | length() | diferentes |<!--html_preserve--><i class="fas  fa-circle " style="color:red;"></i><!--/html_preserve--> <br> <!--html_preserve--><i class="fas  fa-circle " style="color:blue;"></i><!--/html_preserve--> <br> <!--html_preserve--><i class="fas  fa-circle " style="color:green;"></i><!--/html_preserve-->| 


# c()

- Crea un vector

- Según sus elementos será la clase del vector: *character*, *numeric*, *integer*, *logical*

- Cada elemento va separado por una coma

- Con la función **class()** compruebo que tipo de objeto es


# Vector


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


# Vector

Para el caso de "palabras" ("strings"), la clase "character" es la que utiliza R para manejar este tipo de objetos. Al igual que en la mayoría de los lenguajes de programación, R utiliza las comillas 
dobles (") o simples (') para delimitar un string. 

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



# Data frame

- Puede verse como un conjunto de vectores de diferente tipo pero de igual largo.


```r
# vector numeric
x <- c(15, 16, 17, 18)

# vector character
w <- c("lunes", "martes", "miércoles", "jueves")

# data frame
df <- data.frame(x, w)
class(df)
```

```
## [1] "data.frame"
```
- En un conjunto de datos, cada variable/columna es un vector. 


```r
class(df$x); class(df$w)
```

```
## [1] "numeric"
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

## Guardar objeto en formato Rdata


```r
save(h2018, file = "data/ech_h2018.Rdata") #<<
```

El primer elemento debe ser un **objeto**. Podrían ser más de uno.

Es necesario nombrar el argumento **'file'** definiendo ruta y nombre de archivo.

Si en file solo se define el nombre del archivo, se guarda en el directorio de trabajo actual: **getwd()**

El **nombre** del objeto y el archivo pueden coincidir, pero no necesariamente.

Un archivo Rdata es más **liviano** que cualquier otro formato externo.
