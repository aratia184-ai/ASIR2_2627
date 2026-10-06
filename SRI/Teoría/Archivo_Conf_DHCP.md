Encabezado y Comentarios Generales:
```
# dhcpd.conf
```
Indica el nombre del archivo de configuración. En Linux, todo lo que empieza con # es un comentario y el servidor lo ignora; sirve como guía o documentación.   
```
"#" y líneas sucesivas hasta la línea 9:
```   
Son líneas vacías o comentarios informativos que explican que este es un archivo de ejemplo para el servidor ISC DHCP, advirtiendo además que si existe un archivo alternativo en "/etc/ltsp/dhcpd.conf", este último tendrá prioridad.

Opciones Globales Comunes:
```
# option definitions common to all supported networks...
```
Comentario que indica que las siguientes directivas aplican de forma global a todas las redes que soporte el servidor.  
```
option domain-name "example.org";
```
Asigna el nombre de dominio por defecto (example.org) que se entregará a los equipos clientes cuando reciban su configuración de red.   
```
option domain-name-servers ns1.example.org, ns2.example.org;
```
Especifica las direcciones o nombres de los servidores DNS (ns1.example.org y ns2.example.org) que utilizarán los clientes para resolver nombres de dominio.   

Tiempos de Concesión (Lease Times):
```
default-lease-time 600;
```
Define el tiempo predeterminado (en segundos) que un cliente mantiene una dirección IP asignada antes de tener que renovarla. En este caso, 600 segundos (10 minutos).
```
max-lease-time 7200;
```
Define el tiempo máximo (en segundos) que el servidor puede otorgar una IP si el cliente la solicita expresamente. En este caso, 7200 segundos (2 horas).

Actualizaciones Dinámicas de DNS (DDNS):

Comentarios explicativos sobre el parámetro "ddns-update-style", que controla si el servidor DHCP debe intentar actualizar automáticamente los registros DNS cuando se asigna una IP.   
```
ddns-update-style none;
```
Desactiva por completo las actualizaciones dinámicas de DNS (none), imitando el comportamiento de las versiones antiguas de DHCP.   

Servidor Autoritativo:

Comentarios que indican cómo configurar si este servidor es el oficial o principal de la red local.
```
#authoritative;
```
Al estar precedido por #, se encuentra comentado (desactivado). Si se descomentara (quitando el #), le indicaría a la red que este es el servidor DHCP oficial, encargado de rechazar configuraciones erróneas de clientes rápidamente.   

Registro de Eventos (Logs):

Comentarios orientados a la redirección de los mensajes de registro (logs) del servidor hacia un archivo o facilidad específica del sistema de logs (syslog).   
```
#log-facility local7;
```
Está comentado. Si se activara, enviaría los registros del servidor DHCP a la facilidad local7 del sistema de bitácoras.

Declaración de Subred (Subnet):

Comentarios que explican que declarar una subred sin ofrecer servicio en ella ayuda al servidor a comprender la topología de la red.   
```
#subnet 10.152.187.0 netmask 255.255.255.0 {
```
Esta línea de declaración de subred está comentada. Sirve para definir un rango de red específico (en este caso la red 10.152.187.0 con máscara 255.255.255.0). Al tener un # al principio, el servidor no la está aplicando actualmente.   
```
#}
```
Cierra el bloque de la subred anterior, también comentado. 
