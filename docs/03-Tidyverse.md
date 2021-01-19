# Tidyverse

El paquete [tidyverse](https://www.tidyverse.org) es un conjunto de paquetes de R que comparten filosofía de diseño, gramática y estructura de datos. *tidyverse* proporciona una forma unificada, armoniosa y más poderosa de trabajar con datos que la que ofrece el paquete *base*.
Un buen trabajo científico requiere de escribir un código claro y reproducible, este conjunto de paquetes ayudan para que esto sea posible.

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

 <!-- dplyr::summarise() --> 

<!-- Calcula resumen de variables. -->

<!-- Se puede utilizar cualquier función que cumpla con que lo datos de entrada sean numéricos y como salida se entregue una constante. -->

<!-- Si la variable tiene datos faltantes se puede calcular el promedio sin considerarlos -->

<!-- tally -->
<!-- count -->
<!-- add_count -->
<!-- add_tally -->
<!-- fechas -->
