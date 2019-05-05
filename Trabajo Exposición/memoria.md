<p align="center">
  <img src="https://www.redeszone.net/app/uploads/2018/03/Servidores-SAMBA.png?x=634&y=309">
</p>

# Trabajo de Exposición de SWAP - Creación de un servidor Samba para compartición de archivos
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
Nuestro objetivo es montar un servidor Samba para el uso de carpetas compartidas. Esto nos permitirá acceder desde diferentes dispositivos con diferentes sistemas operativos a dichas carpetas, las cuales estarán sincronizadas en todo momento.

Inicialmente nuestra idea era montar un servidor NFS que sirviera para Android, Linux y Windows. Sin embargo, en la App Store prácticamente todas las aplicaciones de gestión de archivos soportaban SMB pero no NFS. Además, hemos leído y buscado sobre las ventajas y desventajas de Samba frente a NFS y parece que Samba es más adecuado cuando se está en un entorno mixto, es decir con diferentes sistemas operativos. También parece ser que NFS es bastante más rápido que Samba cuando se trata de paso de ficheros pequeños.

## Instalación de SMB server en Linux, configuración y prueba.

### Instalación

```PowerShell
$ sudo apt install samba
```

### Configuración:
```PowerShell
$ sudo vi /etc/samba/smb.conf
```
Al final del archivo añadimos un apartado para nuestra sección:

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/fin_share.png">

Ahora creamos la carpeta que hayamos especificado en la sección. 

```PowerShell
$ sudo mkdir -p /srv/samba/share
```

Y reiniciamos el servicio: 

```PowerShell
$ sudo systemctl restart smbd.service nmbd.service
```

En el fichero smb.conf podemos encontrar diferentes apartados. Existe una sección global reservada que especifica características de la configuración global. La sección que hemos añadido nosotros tiene la opción "guest ok = yes" con lo cual cualquier persona en la red podría acceder a dicha carpeta. 

  En caso de querer limitar el acceso a ciertos usuarios deberíamos especificar la opción "valid users", es decir añadiríamos al final de la sección "valid users = juan, pedro, antonio". Ahora solo estarían autorizados estos usuarios. 
  Para añadir usuarios, primeramente debemos crearlos en linux. Luego debemos asignarles una contraseña con smbpasswd. Para juan los comandos serían: 
  
    sudo adduser juan
    
    sudo smbpasswd -a juan
    
    (nos pide contraseña)


También está la posibilidad de que queramos restringir el acceso a un espacio a determinadas máquinas o subredes. La opción a usar sería "hosts allow". Por ejemplo, añadiríamos "hosts allow = 192.168.3.2" en nuestra sección definida si quisiéramos que sólo esa IP pudiera tener acceso a esa sección. También podemos especificar una  subred entera simplemente borrando el último octeto. 
  En la configuración por defecto de samba no hay "hosts allow" definidos en la sección global. Por ello, para cada sección se aplica únicamente la regla que definamos allí. Por tanto, en nuestro caso, "hosts allow = 192.168.3.5"  permitiría el acceso únicamente a dicha IP. Al final hay un enlace a un documento sobre cómo samba calcula las IPs autorizadas a una sección.

Vamos a conectarnos desde tres sistemas operativos diferentes (linux, windows y Android) a la carpeta para ver el correcto y vamos a observar cómo un cambio creado desde un sitio se muestra en los demás.

Primero creemos en la carpeta 4 archivos de ejemplo:

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/touchs.png">

Y ahora vamos a conectarnos:

Para la conexión desde windows recomendamos ir a ejecutar -> \\<ip_sv>. Tras pulsar enter nos debe llevar a la carpeta usando el explorador de archivos. Para saber la IP a la que debemos conectarnos ejecutamos ifconfig en la máquina donde hayamos montado el servidor. 

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/resultado_touchs.png">


Para la conexión desde linux usamos simplemente el explorador. Debajo de equipo veremos "Conectarse con un servidor". Introducimos smb://<ip> y pulsamos enter.

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/resultado_touchs_ubuntu.png">


Para conectarnos desde Ubuntu podemos bajarnos de la App Store un File Manager que pueda conectarse a servidores Samba. Nosotros hemos usado Cx File Explorer (https://play.google.com/store/apps/details?id=com.cxinventor.file.explorer&hl=es)

<img src="https://github.com/davidluque1/SWAP/blob/master/cambios_android.jpeg">

### Samba vs. NFS

### Otros Detalles

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
