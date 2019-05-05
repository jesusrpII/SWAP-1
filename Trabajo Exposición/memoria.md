<p align="center">
  <img src="https://www.redeszone.net/app/uploads/2018/03/Servidores-SAMBA.png?x=634&y=309">
</p>

# Trabajo de Exposición de SWAP - Creación de un servidor Samba para compartición de archivos
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
El objetivo de este trabajo es crear un servidor Samba que permita crear una red de archivos compartidos, al igual que en la práctica 6 de la asignatura en la que se utiliza nfs. Sin embargo, a diferencia de nfs Samba utiliza un protocolo smb la cual es compatible con Windows, esto nos permitirá acceder desde diferentes dispositivos con diferentes sistemas operativos a recursos compartidos, los cuales estarán sincronizados en todo momento. En concreto vamos a probar la conexión con Linux, Windows y Android.


## Instalación de SMB server en Linux, configuración y prueba.

### Instalación

La instalación del servicio en un sistema linux es bastante sencilla, basta con lo siguiente:

```PowerShell
$ sudo apt install samba
```

### Configuración:

Una vez instalado el servidor samba accedemos a la configuración que se encuentra en /etc/samba/smb.conf.

```PowerShell
$ sudo vi /etc/samba/smb.conf
```
Creamos el recurso compartido para ello utilizamos ["nombredelrecurso"] y debajo la configuración que se desee para dicho recurso:

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/fin_share.png">

En el fichero smb.conf podemos encontrar diferentes apartados. Existe una sección global reservada que especifica características de la configuración global. 
En la imagen anterior se ha añadido una sección con una configuración básica en la que path indica la ruta al directorio compartido,browsable indica que es visible desde el buscador de archivos en red, guest ok permite que se pueda acceder al recurso sin usuario ni contraseña, create mask indica los permisos que se otorgan sobre el recurso...
En definitiva creamos un recurso compartido en la red que puede ser editado y accedido por cualquier usuario y equipo en la red.

Ahora creamos la carpeta que hayamos especificado en la sección. 

```PowerShell
$ sudo mkdir -p /srv/samba/share
```

Y reiniciamos el servicio: 

```PowerShell
$ sudo systemctl restart smbd.service nmbd.service
```



En caso de querer limitar el acceso a ciertos usuarios deberíamos especificar la opción "valid users", es decir añadiríamos al final de la sección "valid users = juan, pedro, antonio". Ahora solo estarían autorizados estos usuarios. 
  Para añadir usuarios, primeramente debemos crearlos en linux. Luego debemos asignarles una contraseña con smbpasswd. Para juan los comandos serían: 
  
    sudo adduser juan
    
    sudo smbpasswd -a juan
    
    (nos pide contraseña)


También está la posibilidad de que queramos restringir el acceso a un espacio a determinadas máquinas o subredes. La opción a usar sería "hosts allow". Por ejemplo, añadiríamos "hosts allow = 192.168.3.2" en nuestra sección definida si quisiéramos que sólo esa IP pudiera tener acceso a esa sección. También podemos especificar una  subred entera simplemente borrando el último octeto. 
  En la configuración por defecto de samba no hay "hosts allow" definidos en la sección global. Por ello, para cada sección se aplica únicamente la regla que definamos allí. Por tanto, en nuestro caso, "hosts allow = 192.168.3.5"  permitiría el acceso únicamente a dicha IP. Al final hay un enlace a un documento sobre cómo samba calcula las IPs autorizadas a una sección.

Vamos a conectarnos desde tres sistemas operativos diferentes (linux, windows y Android) a la carpeta para ver el correcto y vamos a observar cómo un cambio creado desde un sitio se muestra en los demás.

Se ha creado en la carpeta 4 archivos de ejemplo:

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/touchs.png">


#### Conexión desde Windows

Para la conexión desde windows recomendamos ir a ejecutar -> \\<ip_delservidor>. Tras pulsar enter nos debe llevar a la carpeta usando el explorador de archivos. Para saber la IP a la que debemos conectarnos ejecutamos ifconfig en la máquina donde hayamos montado el servidor. 

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/resultado_touchs.png">


#### Conexión desde Linux

Para la conexión desde linux usamos simplemente el explorador. Debajo de equipo veremos "Conectarse con un servidor". Introducimos smb://<ip> y pulsamos enter.

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/resultado_touchs_ubuntu.png">


Para conectarnos desde Ubuntu podemos bajarnos de la App Store un File Manager que pueda conectarse a servidores Samba. Nosotros hemos usado Cx File Explorer (https://play.google.com/store/apps/details?id=com.cxinventor.file.explorer&hl=es)

<img src="https://github.com/davidluque1/SWAP/blob/master/cambios_android.jpeg">


### Bibliografía

Conocimiento general y tutoriales:

https://www.varonis.com/blog/cifs-vs-smb/

https://ferhatakgun.com/network-share-performance-differences-between-nfs-smb/

https://www.techrepublic.com/article/how-to-set-up-quick-and-easy-file-sharing-with-samba/

https://eltallerdelbit.com/clientes-smb-samba/

http://www.linuxandubuntu.com/home/how-to-configure-samba-server-and-transfer-files-between-linux-windows

Especificaciones más técnicas de samba: 

https://wiki.samba.org/index.php/Main_Page

https://www.sergio-gonzalez.com/doc/10-ldap-samba-cups-pykota/html/samba-configuracion-samba.html

Host allow, host deny y cómo se calculan las IPs autorizadas:
https://www.oreilly.com/openbook/samba/book/ch04_06.html
