# Proyecto Bastionado 2

En este documento veremos como se puede configurar un sistema informático para que un actor malicioso no pueda alterar la secuencia de arranque con fines de acceso ilegítimo

## Que vamos a ver

Durante esta documentación podremos ver las siguientes configuraciones

    Ocultación del arranque

    Contraseña de arranque

    Copia de seguridad

    Otras opciones de seguridad

## Ocultación del arranque

    Cuando instalamos un sistema operativo Linux se nos instala de serie un gestor de arranque llamado GRUB, este programa tiene algunas brechas de seguridad que un usuario malintencionado puede aprovechar para acceder a ficheros con información sensible. En esta parte de la documentación vamos a ver como podemos evitar el acceso a este para que el sistema arranque directamente.

