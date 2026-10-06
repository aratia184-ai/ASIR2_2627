# Encabezado y Comentarios Generales:
```
# dhcpd.conf
```
Indica el nombre del archivo de configuración. En Linux, todo lo que empieza con # es un comentario y el servidor lo ignora; sirve como guía o documentación.   
```
"#" y líneas sucesivas hasta la línea 9:
```   
Son líneas vacías o comentarios informativos que explican que este es un archivo de ejemplo para el servidor ISC DHCP, advirtiendo además que si existe un archivo alternativo en "/etc/ltsp/dhcpd.conf", este último tendrá prioridad.

# Opciones Globales Comunes:
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

# Tiempos de Concesión (Lease Times):
```
default-lease-time 600;
```
Define el tiempo predeterminado (en segundos) que un cliente mantiene una dirección IP asignada antes de tener que renovarla. En este caso, 600 segundos (10 minutos).
```
max-lease-time 7200;
```
Define el tiempo máximo (en segundos) que el servidor puede otorgar una IP si el cliente la solicita expresamente. En este caso, 7200 segundos (2 horas).

# Actualizaciones Dinámicas de DNS (DDNS):

Comentarios explicativos sobre el parámetro "ddns-update-style", que controla si el servidor DHCP debe intentar actualizar automáticamente los registros DNS cuando se asigna una IP.   
```
ddns-update-style none;
```
Desactiva por completo las actualizaciones dinámicas de DNS (none), imitando el comportamiento de las versiones antiguas de DHCP.   

# Servidor Autoritativo:

Comentarios que indican cómo configurar si este servidor es el oficial o principal de la red local.
```
#authoritative;
```
Al estar precedido por #, se encuentra comentado (desactivado). Si se descomentara (quitando el #), le indicaría a la red que este es el servidor DHCP oficial, encargado de rechazar configuraciones erróneas de clientes rápidamente.   

# Registro de Eventos (Logs):

Comentarios orientados a la redirección de los mensajes de registro (logs) del servidor hacia un archivo o facilidad específica del sistema de logs (syslog).   
```
#log-facility local7;
```
Está comentado. Si se activara, enviaría los registros del servidor DHCP a la facilidad local7 del sistema de bitácoras.

# Declaración de Subred (Subnet):

Comentarios que explican que declarar una subred sin ofrecer servicio en ella ayuda al servidor a comprender la topología de la red.   
```
#subnet 10.152.187.0 netmask 255.255.255.0 {
```
Esta línea de declaración de subred está comentada. Sirve para definir un rango de red específico (en este caso la red 10.152.187.0 con máscara 255.255.255.0). Al tener un # al principio, el servidor no la está aplicando actualmente.   
```
#}
```
Cierra el bloque de la subred anterior, también comentado. 

# Bloque de Subred Básica 1:
```
# This is a very basic subnet declaration.
```
Comentario que indica que el siguiente bloque es un ejemplo de declaración de subred muy básico.   
```
#subnet 10.254.239.0 netmask 255.255.255.224 {
```
Declara una subred (actualmente comentada) con dirección de red 10.254.239.0 y máscara de subred 255.255.255.224 (/27).   
```
# range 10.254.239.10 10.254.239.20;
```
Define el rango de direcciones IP dinámicas que el servidor asignará a los clientes, desde la 10.254.239.10 hasta la 10.254.239.20.   
```
# option routers rtr-239-0-1.example.org, rtr-239-0-2.example.org;
```
Asigna las puertas de enlace predeterminadas (routers) que usarán los equipos de esta subred.   
```
#}
```
Cierra el bloque de esta subred.   

# Bloque para Clientes BOOTP:

"# This declaration allows BOOTP clients to get dynamic addresses", y la línea siguiente comentan que este bloque permite a equipos antiguos basados en BOOTP obtener direcciones dinámicas, aunque no es muy recomendable.   
```
#subnet 10.254.239.32 netmask 255.255.255.224 {
```
Declara otra subred para el segmento 10.254.239.32 con máscara 255.255.255.224.   
```
# range dynamic-bootp 10.254.239.40 10.254.239.60;
```
Establece un rango de IPs reservadas específicamente para asignación dinámica mediante el protocolo BOOTP (del 40 al 60).
```
# option broadcast-address 10.254.239.31;
```
Define la dirección de difusión (broadcast) para esta subred.   
```
# option routers rtr-239-32-1.example.org;
```
Especifica el router o puerta de enlace para los clientes de esta subred.   
```
#}
```
Cierra el bloque de la subred BOOTP.   

# Bloque de Subred Interna con Opciones Personalizadas:
```
# A slightly different configuration for an internal subnet.
```
Comentario que introduce una configuración ligeramente distinta orientada a una red interna.   
```
#subnet 10.5.5.0 netmask 255.255.255.224 {
```
Inicia la declaración de la subred interna 10.5.5.0 con máscara 255.255.255.224.   
```
# range 10.5.5.26 10.5.5.30;
```
Rango de IPs asignables a clientes (del 26 al 30).   
```
# option domain-name-servers ns1.internal.example.org;
```
Servidor DNS específico para esta subred interna.   
```
# option domain-name "internal.example.org";
```
Nombre de dominio específico (internal.example.org) para los equipos de esta red.   
```
# option subnet-mask 255.255.255.224;
```
Reitera la máscara de subred explícitamente para los clientes.   
```
# option routers 10.5.5.1;
```
IP del router principal para esta red (10.5.5.1).   
```
# option broadcast-address 10.5.5.31;
```
Dirección de broadcast para esta subred.   
```
# default-lease-time 600; y # max-lease-time 7200;
```
Sobrescriben los tiempos de concesión de IP (10 minutos por defecto, 2 horas máximo) aplicados de forma exclusiva a esta subred.   
```
#}
```
Cierra el bloque de la subred interna.   

# Declaración de Hosts Especiales:

Las últimas líneas comentadas (# Hosts which require special configuration options can be listed in...) explican que los equipos que necesiten configuraciones especiales (como una dirección IP fija o estática asociada a su dirección MAC) se pueden declarar mediante bloques de tipo host. Si no se especifica una IP fija, se les asigna una dinámica, pero conservando las opciones específicas de esa declaración de host.
