# Tema 1

## Ejercicio 1
**Buscar información sobre las tareas o servicios web para los que se usan más los programas que comentamos al
principio de la sesión (apache, nginx, thttpd, Cherokee, node.js)**

Apache sirve para montar un servidor web, al igual que nginx, salvo que este último puede servir además como balanceadoro proxy para protocolos de correo electrónico.
thttpd sirve también para montar un servidor web, destacando que es mucho más viable para servir grandes volúmenes de información estática. Se dice que es simple, pequeño, portátil, rápido y seguro.
Cherokee es otro servidor web que también permite balanceo de carga y la configuración de servidores virtuales. node.js nos permite ejecutar código javascript basado en eventos en el servidor y se caracteriza por ser muy escalable y tener un gran rendimiento.

# Tema 2

## Ejercicio 1
**Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema)**
![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Ejercicios%20de%20clase/tabla.png)

Lo primero es calcular cuál sería la tabla para 3 elementos. Las fórmulas a usar son:
As = Acn-1 + ( (1 – Acn-1) * Acn ) y As = Ac1 * Ac2 * Ac3 * ... Acn
La tercera tabla sería:

  Web: 97.75 + (1-97.75/100) * 85 = 99.6625
  
  Application: 99 + (1-99/100) * 90 = 99.9
  
  Database: 99.9999 + (1-99.9999/100) * 99.9 = 99.9999999
  
  DNS: 99.96 + (1-99.96/100) * 98 = 99.9992
  
  Firewall: 97.75 + (1-97.75/100) * 85 = 99.6625
  
  Switch: 99.99 + (1-99.99/100) * 99 = 99.9999
  
  Data Center: 99.99 + (1-99.99/100) * 99.99 = 99.999999
  
  ISP: 99.75 + (1-99.75/100) * 95 = 99.9875

  Ahora las multiplicamos: 99.6625/100 * 99.9/100 * 99.9999999/100 * 99.9992/100 * 99.6625/100 * 99.9999/100 * 99.999999/100 * 99.9875/100 = 0.99213515551 -> 99.2% de disponibilidad
  
 ## Ejercicio 2
 **Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2 https://github.com/Unitech/pm2 que sirve para administrar clústeres de NodeJS.**
 
Pm2 es un gestor de procesos en producción para las aplicaciones Node.js que cuenta con un balanceador de carga incorporado. PM2 permite mantener siempre activas las aplicaciones y volver a cargarlas en caso de caída, evitando tiempos de inactividad. También facilita tareas comunes de administrador del sistema y permite monitorizar éste. PM2 también permite gestionar los logs de aplicaciones, su supervisión y cómo están agrupadas.

Otro framework es Express.js, que se podría decir que es el de facto de node.js, y es la librería subyacente para un gran número de otros frameworks web de node.js. 

## Ejercicio 3
**¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor?**


## Ejercicio 4
**Buscar ejemplos de balanceadores software y hardware (productos comerciales).**

https://www.loadbalancer.org/eu?category=products&post-name=hardware&gclid=CjwKCAjw_YPnBRBREiwAIP6TJ8sq8b_rVVd683OdxvCZThrO5-5xK_K2fs0sJro95BArhE6L9RnfUhoC17AQAvD_BwE

Podemos ver diferentes productos. Por ejemplo, el R20 Enteprise ofrece 5 clusters, cada uno con 4 servidores backend, por 3595€. Esto en cuanto a hardware.

En cuanto a software, existen numerosos productos. Buscando rápido encontramos un GSLB de pago:

https://www.pulsesecure.net/resource/global-load-balancing-with-pulse-secure-virtual-traffic-manager/?utm_source=google&utm_medium=cpc&gclid=CjwKCAjw_YPnBRBREiwAIP6TJ04L14ATR12IFkeF93rq_EuguICLFqObEUTOKDgt_--MnSVqYxtHohoC1HYQAvD_BwE

**Buscar productos comerciales para servidores de aplicaciones.**

Para servidores de aplicación, existe Oracle WebLogic Application Server, IBM WebSphere Application Server, 


**Buscar productos comerciales para servidores de almacenamiento.**

Aquí no sé si se refiere a software para gestionar almacenamiento o a almacenamiento en sí. Un ejemplo de almacenamiento: 

https://www.host.ag/storage-servers?utm_campaign=1781974517&utm_source=google&utm_medium=cpc&utm_content=343762872392&utm_term=storage%20servers&adgroupid=71970405514&gclid=CjwKCAjw_YPnBRBREiwAIP6TJ_kQLPoKL_OiCA38PxxhXvrW5IXzgSAlBZ_TFEOnYPEnm0SQGg2UNRoCNhwQAvD_BwE

https://news.cherryservers.com/limited-deal-for-storage-servers?gclid=CjwKCAjw_YPnBRBREiwAIP6TJ-LCFDNA6LNowyp99UUFlqZlJS_teWWa98G_klZgo1NUiHfqPo8kxRoC8HoQAvD_BwE


# Tema 3

## Ejercicio 1 
**Buscar con qué órdenes de terminal o herramientas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.**

En linux haría esto:

    echo 1 > /proc/sys/net/ipv4/ip_forward
    iptables -A FORWARD -i wlan1 -o wlan0 -j ACCEPT
    iptables -A FORWARD -i wlan0 -o wlan1 -m state --state ESTABLISHED,RELATED \
             -j ACCEPT
    iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE

Y en windows esto:
  Instalamos RINETD, creamos un fichero de configuración donde lo hayamos extraido y ponemos como línea: 0.0.0.0 80 192.168.100.1 80. La sintaxis es <source> <port> <destination> <port>. Esto enrutaría todo el tráfico del puerto 80 a 192.168.100.1. Luego ejecutaríamos el proceso: C:\Folder\Where\You\Extracted\rinetd>rinetd.exe -c config.cfg
  
## Ejercicio 2 
**Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**

En linux podemos usar IPtables. En windows podemos usar el firewall, que cuenta con interfaz gráfica.

# Tema 4


## Ejercicio 1
**Buscar información sobre cuánto costaría en la actualidad un mainframe que tuviera las mismas prestaciones que una granja web con balanceo de carga y 10 servidores finales (p.ej). Comparar precio y potencia entre esa hipotética máquina y la granja web de unas prestaciones similares.**
Tras un tiempo buscando, me ha sido imposible encontrar información exacta sobre la capacidad de cómputo total de un mainframe y su precio de forma segura como para poder compararla con servidores de menor escala, en parte ya que IBM no pone precios directamente en su página web. Sí es cierto que los mainframes de IBM parecen costar de $40,000 para arriba. Los servidores de menor escala que he buscado suelen costar entre 1300-3000€. Diría que renta un mainframe sólo si necesitamos procesar un volumen de datos muy grande. Hasta llegar a ese punto renta mucho más servidores corrientes. 

## Ejercicio 2

**Buscar información sobre precio y características de balanceadores comerciales (hardware) específicos.**

https://www.loadbalancer.org/eu?category=products&post-name=hardware&gclid=CjwKCAjw_YPnBRBREiwAIP6TJ_eO1vUtwNsGNB6ThvB5g_DZF6LxwwczLlabjgTzmURwht5xr0kvcxoCpQ8QAvD_BwE

https://kemptechnologies.com/es/server-load-balancing-appliances/product-matrix.html

Pongamos que tenemos unos 12.000€. En loadbalancer adquiriríamos el Enterprise Ultra y en kempt el LM-X15. En "Application Throughput" ganaría LoadBalancer, si bien es cierto que nos costaría 2.000€ y que la mejora no sería algo desorbitado, sino algo ligero. En L7 concurrent connections ganaría de lejos LoadBalancer (1,200,000 frente a 262,500). El producto de LoadBalancer tiene la mitad de ram, sin embargo.

## Ejercicio 4

**Buscar información sobre los métodos de balanceo queimplementan los dispositivos recogidos en el ejercicio 4.2 (o el software que hemos propuesto para la práctica 3).**

Round robin -- Planificación por round robin (turnos), de forma secuencial.
Weighted round robin -- Como round robin, pero asignando un peso a cada servidor. P.ej el servidor A sirve 3x más que el B.
Least connection -- La siguiente petición debe ser procesada por el servidor con menor nº de conexiones.
Weighted least connection -- Al igual que least connection, pero añadiendo un peso a cada servidor
Fixed weighted -- O por prioridad. Los servidoers tienen asignada una prioridad, y las peticiones van al servidor de mayor prioridad. Si éste falla, las peticiones van al 2º con mayor prioridad.
Weighted response -- Basado en el tiempo de respuesta
Source IP hash -- Usando Hashes de IP se determina qué servidor atenderá la petición


## Ejercicio 6
**Buscar información sobre los bloques de IP para los distintos países o continentes. Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario.**

Sobre los bloques:
![Imagen1](https://blog.ip2location.com/wp-content/uploads/2018/12/ipv4_address_map_2016_overlay.png)

Para ver de dónde se conecta un usuario usamos la API de iplocate:

https://www.iplocate.io/

El código php es simple:

    <?php
    $res = file_get_contents('https://www.iplocate.io/api/lookup/46.7.3.29');
    $res = json_decode($res);

    var_dump($res);
?>

Lo he probado en una página web personalizada con ese simple código y es sencillo obtener los datos dada una IP:

![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Ejercicios%20de%20clase/php_zona.png)


## Ejercicio 7
**Buscar información sobre métodos y herramientas para implementar GSLB.**


# Tema 5

## Ejercicio 1

**Buscar información sobre cómo calcular el número de conexiones por segundo.**

Podríamos instalar un módulo para apache2 del tipo server-status que nos diera los request/seg y de ahí obtener las conexiones/seg. Para habilitar el módulo editamos el fichero de configuración mostrado:
![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Ejercicios%20de%20clase/conexiones_seg.png)

## Ejercicio 2

**Revisar los análisis de tráfico que se ofrecen en: http://bit.ly/1g0dkKj. Instalar wireshark y observar cómo fluye el tráfico de red en uno de los servidores web mientras se le hacen peticiones HTTP… o en la red de casa**

![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Ejercicios%20de%20clase/wireshark_web.png)

Paquetes 1-3: 3 way handshake para establecer la conexión
Paquetes 19-22: finalización de la conexión en 4 pasos
Paquete 9: Respuesta OK del servidor 
Resto: contenido

## Ejercicio 3

**Buscar información sobre características, funcionalidad, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor**

# Tema 6

## Ejercicio 1

**Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.
Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.**

Ya lo hicimos en prácticas


## Ejercicio 2

**Comprobar qué puertos tienen abiertos nuestras máquinas, su estado, y qué programa o demonio lo ocupa.**
Es sencillo con el comando netstat -peanut:
![Imagen1](https://github.com/davidluque1/SWAP/blob/master/Ejercicios%20de%20clase/puertos.png)

(vemos como apache2 usa el 80)


## Ejercicio 3

**Buscar información acerca de los tipos de ataques más comunes en servidores web (p.ej. secuestros de sesión). Detallar en qué consisten, y cómo se pueden evitar.**

1 -> Ataques DDOS. Los hay de diferentes tipos y consisten en hacer el servidor inaccesible, bien porque saturan las conexiones que el router puede manejar o bien porque crashean el servidor. La solución general es situar los servidores tras un firewall.

2 -> Man-in-the-middle (MitM) attack. Consiste en suplantar la identidad de algún cliente conectado al servidor, de forma que nos ponemos entre ellos. El uso de protocolos seguros y la encriptación de los datos puede ayudar a prevenir ciertos ataques. 

3 -> Inyecciones SQL. Consisten en ejecutar sentencias SQL del servidor usando formularios inseguros. Son prevenibles usando "prepared statements".

4 -> Cross-site scripting (XSS) attack. Consiste en inyectar un script malicioso en una página web que un visitante ejecutará al visitar la página. Es prevenible teniendo un servidor web seguro y no dejando que terceros puedan inyectar dichos scripts maliciosos.

5 -> Phising. Creación de una página web idéntica a otra, pero a la que tenemos acceso. Cuando una víctima introduzca datos en nuestra página, nos llegarán a nosotros

# Tema 7
**Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.**

1. NT File System (NTFS)

NTFS is es el sistema de ficheros usado por las versiones recientes de Windows. Tiene características modernas que no tienen exFAT ni FAT32. NTFS permisos de ficheros para seguridad, un "journal" para recuperarse de errores si el PC crashea, copias fantasma para backups, encripción, cuotas de disco duro, etcétera. Es compatible con todas las versiones de windows, y es de sólo lectura por defecto en MacOS y algunas distribuciones de linux. Su uso ideal es cuando el dispositivo vaya a usar el sistema operativo Windows.


2. FAT32

FAT32 es el sistema de archivos más antiguo de los tres de windows. Los ficheros en este SA no pueden superar los 4GB y la partición en sí no puede superar los 8TB. Las versiones modernas de FAT32 no pueden instalarse en dispositivos con FAT32. FAT32 funciona con prácticamente cualquier sistema operativo: linux, windows, mac. Por ello, su uso es recomendado si tenemos una serie de archivos guardados y necesitamos la máxima compatibilidad con cualquier sistema operativo. 

3. ext4

ext4 nació como un sistema de ficheros compatible hacia atrás con ext3, con el fin de extender límites de almacenamiento y mejorar ciertos aspectos relacionados con el rendimiento. Entre las ventajas están: podemos manejar el espacio de forma aisalda entre aplicaciones, podemos montar, desmontar, defragmentar o monitorear el rendimiento de SA de forma independiente, y podemos encriptar volúmenes. Las desventajas son que usa más recursos, que hay más posibilidad de malgastar espacio y más posibilidad de avisos de disco lleno, así como que será más difícil conseguir espacio para un volumen quitándoselo a otro.

4. APFS

Apple File System se lanzó en marzo de 2017 como un sustituto a HFS+, usado desde 1998. Entre sus ventajas encontramos: clonación eficiente de archivos usando deltas, soporte de snapshots, encripción con diferentes opciones, integridad de metadatos y protección a caídas, entre otras. Entre las desventajas cabe destacar que no permite la compresión ni hace comprobaciones de los datos almacenados, sólo de metadatos.

# Bibliografía y páginas consultadas

## Tema 1
https://es.wikipedia.org/wiki/Thttpd
https://es.wikipedia.org/wiki/Cherokee_(servidor_web)
https://www.netconsulting.es/blog/nodejs/

## Tema 2

https://www.netconsulting.es/blog/nodejs/
https://en.wikipedia.org/wiki/PM2_(software)

https://www.trustradius.com/application-server

## Tema 3

https://serverfault.com/questions/431593/iptables-forwarding-between-two-interface

https://ma.ttias.be/tcp-traffic-redirection-on-windows/

https://www.quora.com/How-do-I-block-all-TCP-packets-to-a-specific-IP-address-from-my-Windows-10-computer

## Tema 4

https://www.suse.com/c/mainframe-versus-server-farm-comparison/

https://bits.blogs.nytimes.com/2013/07/23/mainframe-computers-that-change-with-the-times/

https://www.techopedia.com/definition/31290/load-balancing-methods

https://www.iplocate.io/

## Tema 5

## Tema 6

https://askubuntu.com/questions/278448/how-to-know-what-program-is-listening-on-a-given-port

https://blog.netwrix.com/2018/05/15/top-10-most-common-types-of-cyber-attacks/

## Tema 7

https://www.ufsexplorer.com/articles/file-systems-basics.php

https://en.wikipedia.org/wiki/Comparison_of_file_systems

https://www.geeksforgeeks.org/difference-fat32-exfat-ntfs-file-system/
