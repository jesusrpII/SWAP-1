# Práctica 2 de SWAP
Pareja para la práctica: David Luque y Jesús Rodríguez

## Objetivo
Instalar rsync y hacer que las máquinas tengan los directorios /var/www/ sincronizados (que tengan el mismo contenido).

## Procedimiento
Hace falta permitir el acceso automático de SSH, para lo que se debe generar una clave en la máquina 2 y copiarla en la máquina 1. Una vez esto está hecho, se añade una línea a crontab que ejecute un comando de rsync cada hora. Este comando copiará el contenido de /var/www/ en la máquina1 a /var/www/ en la máquina 2 (máquina en la que se ejecuta el comando).

## Imágenes

### Instalamos rsync y creamos una clave pública en máquina 2
![Instalamos rsync y creamos una clave pública en máquina 2](https://github.com/davidluque1/SWAP/blob/master/Practica%202/pract2_inicio.png)
Nota: rsync también está instalado en la máquina 1

### Copiamos la llave creada en la máquina 2 a la máquina 1
![Copiamos la llave creada en la máquina 2 a la máquina 1](https://github.com/davidluque1/SWAP/blob/master/Practica%202/pract2_copy_key.png)

### Hacemos al usuario de la máquina 2 dueño de /var/www/ en la máquina 2 y probamos rsync a la máquina 1:
![Copiamos la llave creada en la máquina 2 a la máquina 1](https://github.com/davidluque1/SWAP/blob/master/Practica%202/pract2_permisos.png)

### Editamos en la máquina 2 el archivo crontab para automatizar la copia
![Editamos en la máquina 2 el archivo crontab para automatizar la copia](https://github.com/davidluque1/SWAP/blob/master/Practica%202/pract2_crontab.png)

