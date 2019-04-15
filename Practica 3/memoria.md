# Práctica 3 de SWAP
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
Configurar haproxy y nginx como balanceadores de carga. Comprobar que se distribuye la carga usando htop en los servidores.

## Procedimiento
Para la realización de la práctica hemos utilizado dos máquinas virtuales maq1 (192.168.56.105) y maq2 (192.168.56.106) como servidores que procesan peticiones. maq3 (192.168.56.107) corresponde al balanceador nginx y maq4 (192.168.56.108) corresponde al balanceador haproxy

### nginx

La configuración de nginx usada ha sido: 
![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Practica%203/pract3_nginx_config.png)

Mostramos que la carga se reparte. Para ello, desactivamos la sincronización entre máquinas y cambiamos el fichero index.html en cada una:
![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Practica%203/pract3_nginx_alterna.png)

Para someter al servidor balanceador (192.168.56.107) a una alta carga usamos ab:

ab -n 500000 -c 10 http://192.168.56.107/index.html

La carga se distribuye correctamente. Lo hemos comprobado usando el comando htop:
![Imagen2](https://github.com/davidluque1/SWAP/blob/master/Practica%203/pract3_nginx_htop.png)

### haproxy

La configuración de haproxy ha sido:

![Imagen2](https://github.com/davidluque1/SWAP/blob/master/Practica%203/pract3_haproxy_config.png)

La carga se distribuye correctamente si usamos el comando htop:
![Imagen2](https://github.com/davidluque1/SWAP/blob/master/Practica%203/pract3_nginx_htop.png)


