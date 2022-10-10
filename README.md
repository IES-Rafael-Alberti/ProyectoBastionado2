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

