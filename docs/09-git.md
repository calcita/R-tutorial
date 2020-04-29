# Control de versiones

Un programa de control de versiones mantiene una copia de los cambios en el código u otro contenido. Esto es útil en caso de que necesitemos revertir algún cambio realizado.  

Seguramente todxs hemos implementado un control de versiones en nuestros proyectos. Por ejemplo, haciendo una tesis y nombrando por fecha al archivo hasta acumular decenas de archivos similares. Esto es un caos y nos brinda una falsa seguridad de que podremos recuperar algo que quitamos o cambiamos. ¿En qué versión estará? ¿En la del 10 de marzo o la del 11? 

![](images/tesis.png)
Si usamos una plataforma como Dropbox estamos en una situación similar, contamos con un historial de archivos en caso de necesitarlo. O con Google Docs tenemos la opción de "version history" que viene a ser algo similar. Una ventaja de Google Docs respecto a Dropbox es que permite editar un mismo documento por varias personas a la vez.

Pero ninguno de estos métodos de control de versiones es lo suficientemente eficiente y menos cuando de programar se trata. Por ello, existen software específicos para el control de versiones, uno de los más populares es git. 

¿Por qué es importante un software de contorl de versiones? Para revertir un cambio realizado y poder trabajar colaborativamente sobre un mismo proyecto sin preocuparnos que alguien borre algún archivo o parte del mismo. Nada se pierde, todo se recupera ... ¿quiénes pensaron en la frase de Drexler? :notes:

Para trabajar con otras personas en un mismo proyecto, es decir, sobre los mismos archivos debemos alojar una copia de estos archivos en un web server que oficia de nube. Dentro de los más populares se encuentran github y gitlab. Así GitHub o Gitlab proporcionan una copia de seguridad de tu trabajo que se puede recuperar si se pierde tu copia local, es decir, aquella que está en computadora. 

Por lo tanto, usar git conjuntamente con Github o Gitlab nos proporciona lo siguiente:

- realizar un seguimiento de los cambios en tu código localmente
- sincronizar entre diferentes versiones de los archivos, esto es, entre tus propias versiones o las de otras personas.
- probar cambios en el código sin perder una versión anterior.
- respaldar tus archivos en la nube (github.com o gitlab.com) 
- compartir tus archivos en la web (github.com o gitlab.com) 

## ¿Qué es git?

Hagamos una analogía entre git y el e-mail. 

E-mail es un protocolo para enviar mensajes online, independientemente de cual servidor de e-mail uses (gmail, hotmail, adinet, etc.).

Git es un protocolo para compartir versiones de tu código, independientemente de cual servidor git uses (github, gitlab, bitbucket).


Así github.com es a git lo que gmail.com es a e-mail.

## Clonar

## Commit

### Primer commit

## Push

## Pull


   #edf8b1
   
div.blue { background-color:#efedf5; border-radius: 5px; padding: 20px;}
</style>
<div class = "blue">

![](images/document.png){ width=2% } **Objetivos**

Después de completar esta lección serás capaz de:

Explicar como gihub y git usan los repositorios para alojar y manejar archivos.
Usar el comando git clone para bajar una copia del repositorio a tu computadora.
    
**Requisitos** 

Haber completado la sección de configuración de Git en tu computadora

Haber creado una cuenta en Github.com y recordar usuario y contraseña.

</div>

## Crear un proyecto en gitlab

<iframe src="https://player.vimeo.com/video/292637965" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>


## Crear un repositorio en github

## Instalar git

git es el software de control de versiones. En distribuciones Linux suele venir instalado. En Windows se instala a través del ejecutable.


## Configurar git en Rstudio

<iframe src="https://player.vimeo.com/video/292760320" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

## Commit y push

Para enviar los cambios que realizamos localmente primero debemos seleccionar los archivos modificados, creados o eliminados, luego hacer commit para lo cual es necesario escribir un mensaje que describa los cambios que realizamos. 

<iframe src="https://player.vimeo.com/video/292639340" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

Para que un mensaje del commit nos resulte útil debe describir brevemente lo que hicimos y no haber hecho muchas cosas antes de hacer un commit. Podemos volver a una versión anterior del código y para saber a cuál resulta muy útil ese mensaje.


## Pull

Descargar los cambios que otra persona o yo misma desde otra computadora realicé.

<!-- #b2e2e2 -->

![](images/idea.png){ width=2% } 
Importante

## Historial


## .gitignore
<style>
div.blue { background-color:#edf8b1; border-radius: 5px; padding: 20px;}
</style>
<div class = "yellow">

![](images/work.png){ width=2% } **Ejercicio**


</div>


:::puzzle
My content goes in here!
:::
