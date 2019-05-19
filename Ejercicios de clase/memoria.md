# Tema 1

## Ejercicio 1
**Buscar información sobre las tareas o servicios web para los que se usan más los programas que comentamos al
principio de la sesión (apache, nginx, thttpd, Cherokee, node.js)**

Apache sirve para montar un servidor web, al igual que nginx, salvo que este último puede servir además como balanceadoro proxy para protocolos de correo electrónico.
thttpd sirve también para montar un servidor web, destacando que es mucho más viable para servir grandes volúmenes de información estática. Se dice que es simple, pequeño, portátil, rápido y seguro.
Cherokee es otro servidor web que también permite balanceo de carga y la configuración de servidores virtuales. node.js nos permite ejecutar código javascript basado en eventos en el servidor y se caracteriza por ser muy escalable y tener un gran rendimiento.

# Tema 2

##Ejercicio 1

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


# Tema 3



# Tema 4



# Tema 5



# Tema 6



# Tema 7


#Bibliografía

## Tema 1
https://es.wikipedia.org/wiki/Thttpd
https://es.wikipedia.org/wiki/Cherokee_(servidor_web)
https://www.netconsulting.es/blog/nodejs/

## Tema 2

## Tema 3

## Tema 4

## Tema 5

## Tema 6
