<p align="center">
  <img src="https://www.redeszone.net/app/uploads/2018/03/Servidores-SAMBA.png?x=634&y=309">
</p>

# Trabajo de Exposición de SWAP - Creación de un servidor Samba para compartición de archivos
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
Nuestro objetivo es montar un servidor Samba para el uso de carpetas compartidas. Esto nos permitirá acceder desde diferentes dispositivos con diferentes sistemas operativos a dichas carpetas, las cuales estarán sincronizadas en todo momento.

### Instalación de SMB server en Linux, configuración y prueba.

####Instalación

```PowerShell
$ sudo apt install samba
```

####Configuración:
```PowerShell
$ sudo vi /etc/samba/smb.conf
```
Al final del archivo añadimos un apartado para nuestra sección:

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/share.png">

Ahora creamos la carpeta que hayamos especificado en la sección. 

```PowerShell
$ sudo mkdir -p /srv/samba/share
```

Y reiniciamos el servicio: 

```PowerShell
$ sudo systemctl restart smbd.service nmbd.service
```
####Conexión
Para la conexión desde windows recomendamos ir a ejecutar -> \\<ip_sv>. Tras pulsar enter nos debe llevar a la carpeta usando el explorador de archivos: 

<img src="https://github.com/davidluque1/SWAP/blob/master/ejecutar.png">

Para la conexión desde linux usamos simplemente el explorador: 

<img src="https://github.com/davidluque1/SWAP/blob/master/Trabajo%20Exposici%C3%B3n/acceso_linux.png">

