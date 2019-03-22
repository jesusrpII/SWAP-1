# Práctica 2 de SWAP
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
Configuración de las máquinas en modo espejo de manera que la segunda máquina contenga y actualice automáticamente el contenido del directorio /var/www/ de la primera máquina.

## Procedimiento
Para la realización de la práctica hemos utilizado dos máquinas virtuales ubuntuswap (192.168.1.100) y ubuntuswap2 (192.168.1.101)

### Copiar de archivos por ssh
Siguiendo las indicaciones del guión hemos probado la copia de archivos de la máquina 1 a la 2 utilizando tar mediante ssh:

![Imagen1](tar1.png)

Comprobamos que la copia se ha realizado correctamente en la máquina 2:

![Imagen2](tar2.png)

### Funcionamiento de rsync

Hemos instalado rsync mediante el comando sudo apt-get install rsync (en nuestro caso ya se encontraba instalado en las máquinas).

Ahora desde la máquina 2 hemos clonado el directorio /var/www/ de la máquina 1 (en el directorio /var/www/ de la máquina 2):

![Imagen3](rsync1.png)


En la anterior imagen al tener el mismo contenido las dos máquinas no nos notifica ningún cambio, en cambio si modificamos en la máquina 1 podemos observar como al clonar se nos notifica en la máquina 2:

![Imagen4](rsync2.png)

(En la imagen anterior hemos creado previamente un directorio en la máquina 1 /var/www/html/prueba )





### Configuración de ssh para acceder sin que se solicite contraseña
Todo este proceso se realizará desde la máquina 2, primero creamos la clave pública y privada mediante el siguiente comando y a continuación copiamos la clave pública en la máquina 1:

![Imagen5](clavessh.png)

Comprobación de que ahora podemos acceder desde la máquina 2 a la 1 sin contraseña:

![Imagen6](sshsincontra.png)

### Automatización del proceso utilizando cron
Basta con modificar el archivo /etc/crontab de la siguiente forma (solo se a añadido la última línea):

![Imagen7](crontab.png)

Se ejecutara el comando cada hora de cada dia al minuto 0.



## Resumen
Se ha configurado ssh para permitir que la segunda máquina pueda acceder a la primera sin necesidad de contraseña, una vez conseguido con rsync podemos clonar cualquier directorio a la máquina 1 (ya sinintroducir contraseña) y por último se ha automatizado el proceso utilizando /etc/crontab de manera que la clonación se realice cada hora.

