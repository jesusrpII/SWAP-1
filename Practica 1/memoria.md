# Práctica 1 de SWAP
Pareja para la práctica: David Luque y Jesús Rodríguez

## Objetivo
Instalar dos máquinas virtuales con ubuntu server 16 y establecer conexión entre ellas con curl y ssh

## Procedimiento
Se crean dos máquinas virtuales con la imagen correspondiente y todos los valores por defecto. En mi caso he añadido una red sólo-anfitrión y he añadido las líneas correspondientes a /etc/network/interfaces

## Imágenes

### Curl e ifconfig
Mediante ifconfig podemos ver la ip de ambas máquinas, el de la máquina 1 será 192.168.1.105 y el de la máquina 2 192.168.1.106 (para ello hemos modificado el correspondiente archivo que comentaremos a continuación). Mediante curl hemos obtenido el código html de un fichero hola.html de la máquina 1 desde la 2 y viceversa.
![Curl e ifconfig](https://github.com/davidluque1/SWAP/blob/master/SWAP_pract2_img2.png)

### Conexión ssh
Hemos comprobado en este apartado la conectividad ssh entre ambas máquinas con los comandos que se pueden observar en la captura.
![SSH entre dos máquinas](https://github.com/davidluque1/SWAP/blob/master/SWAP_pract1_img.png)

### /etc/network/interfaces
Configuración usada para la interfaz creada enp0s8 en cada máquina.
![/etc/network/interfaces](https://github.com/davidluque1/SWAP/blob/master/SWAP_pract1_img4.png)
