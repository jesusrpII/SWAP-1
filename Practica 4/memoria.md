
# Práctica 3 de SWAP
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
Instalar un certificado SSL para configurar el acceso por HTTPS a los servidores, y configurar reglas del cortafuegos para proteger la granja web

## Procedimiento
Para la realización de la práctica hemos utilizado dos máquinas virtuales maq1 (192.168.56.105) y maq2 (192.168.56.106) como servidores que procesan peticiones, así como maq3 (192.168.56.107) como balanceador nginx

### Instalar certificado: comandos
Hemos seguido el guión e introducido los comandos especificados:

```PowerShell
a2enmod ssl
service apache2 restart
mkdir /etc/apache2/ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout
 /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
 a2ensite default-ssl
service apache2 reload
```

Para copiar los .crt y .key de la máquina 1 a las demás, hemos usado scp <origen> <destino>

![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Practica%204/p5_scp.png)


### Instalar certificado: ficheros de configuración
En cuanto a ficheros, mostramos cómo nos quedó /etc/apache2/sites-available/default-sites-available/default-ssl.conf en las máquinas:

![Imagen2](https://github.com/davidluque1/SWAP/blob/master/Practica%204/p5_sites_available.png)

En el balanceador hemos modificado también este fichero: 

![Imagen3](https://github.com/davidluque1/SWAP/blob/master/Practica%204/p5_balanceador_default.conf.png)

Añadir también que los certificados en el balanceador (maq3) están en carpetas diferentes que en las máquinas finales (maq1 y maq2)

### Instalar certificado: prueba en el balanceador

Si bien esto ya se mostró en clase, mostramos una petición https al balanceador:

![Imagen3](https://github.com/davidluque1/SWAP/blob/master/Practica%204/p5_https_balanceador.png)

### IPtables: configurar el cortafuegos

Para configurar el cortafuegos hemos simplemente seguido el guión y editado el fichero rc.local, de forma que al inicio del sistema se ejecuten órdenes que configuren correctamente las conexiones que permitimos y las que denegamos. 

![Imagen3](https://github.com/davidluque1/SWAP/blob/master/Practica%204/p5_local.rc.png)

Las dos líneas añadidas al final abren el puerto 443 como entrada y salida, para permitir conexiones HTTPS.
