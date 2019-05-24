# Práctica 5 de SWAP
Integrantes del grupo: David Luque y Jesús Rodríguez

## Objetivo
Configurar dos máquinas de manera que se mantega actualizada la información en una base de datos entre dos servidores (un servidor secundario actualizará la información del servidor principal)

## Procedimiento
Para la realización de la práctica hemos utilizado dos máquinas virtuales maq1 (192.168.56.105) y maq2 (192.168.56.106) 

### Creación de una base de datos
Hemos seguido el guión y hemos creado una base de datos en la máquina 1:

![Imagen1](https://github.com/jesusrpII/SWAP/blob/master/Practica5/p5_creardb.png)
(Previamente se ha creado una base de datos llamada contactos)

### Realizar copia de seguridad utilizando mysqldump y copiar los archivos en la máquina secundaria

Copia de seguridad en máquina 1 (servidor principal):

![Imagen2](https://github.com/jesusrpII/SWAP/blob/master/Practica5/p5_mysqldump.png)



Copiamos la copia de seguridad con scp en la máquina 2:

![Imagen3](https://github.com/jesusrpII/SWAP/blob/master/Practica5/p5_copiardb.png)



### Restaurar la copia de seguridad en la máguina 2

Tras copiar el archivo de copia de seguridad en la máquina 2 utilizamos:

![Imagen4](https://github.com/jesusrpII/SWAP/blob/master/Practica5/p5_restaurardb.png)

Como se puede observar la restauración es correcta, la base de datos es idéntica a la anteriormente creada en máquina1.



### Realizar configuración maestro-esclavo de los servidores MySQL

Para que la replicación de datos se realice automáticamente hemos configurado la máquina 1 como maestro y la máquina 2 como esclavo.Hemos modificado el archivo de configuración de mysql /etc/mysql/mysq.conf.d/mysqld.cnf y creamos un usuario esclavo con privilegios de acceso en la máquina principal y introducimos los datos sobre el host en la máquina 2 (máquina esclavo) tal como indica el guión y comprobamos el estado: 
![Imagen5](https://github.com/jesusrpII/SWAP/blob/master/Practica5/p5_mysqlstatus.png)

Tras ver el estado de MASTER y SLAVE parece que funciona todo,comprobamos creando un par de tablas (prueba1 y prueba2) que en todo momento la máquina 2 contiene la misma información que la máquina 1:

![Imagen6](https://github.com/jesusrpII/SWAP/blob/master/Practica5/p5_mysqlcomprobar.png)

En la imagen anterior se puede observar como se va actualizando la base de datos de la máquina 1 y la máquina 2 se mantiene actualizada en todo momento.
