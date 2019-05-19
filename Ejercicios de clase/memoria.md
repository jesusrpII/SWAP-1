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

**Buscar información sobre los métodos de balanceo queimplementan los dispositivos recogidos en el ejercicio 4.2 (o el software que hemos propuesto para la práctica 3). **

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



# Tema 6



# Tema 7


#Bibliografía

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
