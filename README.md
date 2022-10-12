author: Pablo Crespo Cervantes
summary: Resumen del CodeLab 
id: identificador-unico-del-codelab 
categories: codelab,markdown 
environments: Web 
status: Published 
feedback link: Un enlace en el que los usuarios puedan darte feedback (quizás creando un issue en un repositorio de git) 
analytics account: ID de Google Analytics 
 

# Proyecto Bastionado 2

## Que vamos a ver

En este documento veremos como se puede configurar un sistema informático para que un actor malicioso no pueda alterar la secuencia de arranque con fines de acceso ilegítimo

Durante esta documentación podremos ver las siguientes configuraciones:

- Ocultación del arranque
- Contraseña de arranque 
- Copia de seguridad
- Otras opciones de seguridad

</ul>

<br>

## Ocultación del arranque

Cuando instalamos un sistema operativo Linux se nos instala de serie un gestor de arranque llamado GRUB, este programa tiene algunas brechas de seguridad que un usuario malintencionado puede aprovechar para acceder a ficheros con información sensible. En esta parte de la documentación vamos a ver como podemos evitar el acceso a este para que el sistema arranque directamente.

Es recomendable hacer una copia de seguridad de los archivos que vamos a modificar para mantener los originales por si surgiera algun problema, podemos realizarlos usando el siguiente comando si estamos en el directorio: 
<br>
```sh
cd /etc/default
cp grub grub.backup
```
<br>
Para ocultar el arranque deberemos de modificar la linea de comando que veremos a continuacion en el fichero /etc/grub.d/30_os-prober

Insertar imagen 1
![This is an image](https://github.com/IES-Rafael-Alberti/ProyectoBastionado2/blob/main/img/imagengrub1.png)



Por ultimo modificaremos el fichero /etc/default/grub, y cambiaremos las lineas Grub_Timeout = 10 y  GRUB_DISABLE_OS_PROBER tal como vemos en la siguiente imagen


una vez terminado y guardado los cambios podemos ejecutar sudo update-grub para que los cambios se efectuen.

## Contraseña de arranque

El siguiente metodo de securización que utilizaremos sera la implantación de una contraseña en el arranque la cual se nos pedira cuando intentemos iniciar el equipo.

Lo primero que haremos para la configuración sera generar una contraseña segura que utilizaremos en el arranque para ello utilizaremos un comando que tiene grub el cual nos generara una contraseña con hash a partir de la que pongamos nosotros como usuarios.

```sh
grub-mkpasswd-pbkdf2
```

como podemos ver en la siguiente imagen una vez escribamos la contraseña nos aparecera el resultado.

insertar imagen 3

Una vez tenemos esta contraseña podemos ir al fichero /etc/grub.d/40_custom para añadir las siguientes lineas que nos permitiran configurar el usuario con la contraseña generada anteriormente

insertar imagen 4

Por ultimo tendremos que hacer un update a grub para que se almacenen los cambios que hemos realizado en los ficheros anteriormente mencionados, para ello utilizaremos el comando

```sh
update-grub
```
Insertar imagen 5

Como podemos ver al reiniciar tras actualizar grub nos aparecera la ventana de inicio de sesión (especifica de grub).

Insertar imagen 6

#### Configurar usuario

Hemos visto como generar un superusuario con contraseña el cual nos permitira proteger grub pero es posible segun la configuracion que estemos haciendo que solo queramos generar un usuario normal para ello deberemos seguir los mismos pasos pero tendremos que modificar la entrada de menu para darle acceso al usuario con el que estemos trabajando.

Vamos a crear otro usuario dentro del fichero 40_custom pero esta vez usaremos una contraseña con texto plano para comprobar que tambien funciona.

Insertar imagen 7

Tras esto iremos al fichero de configuracion 10_linux donde estan las menuentry 

## Copia de seguridad Grub

Para crear una copia de seguridad actualmente debemos de copiar/restaurar varios archivos, antiguamente con grub solo hacia falta recuperar errl archivo /boot/grub/menu.lst pero con grub 2 deberemos de recuperar los siguientes archivos/directorios

- /etc/default/grub
- /etc/grub.d/
- /boot/grub/grub.cfg

podremos hacer un tar de estos archivos o programar un pequeño script que automatice esta tarea.

insertar imagen 9

