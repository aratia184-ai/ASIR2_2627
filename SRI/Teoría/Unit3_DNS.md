# DNS 

El DNS funciona como la "agenda de contactos" de Internet.

Para que entiendas cómo trabaja y por qué es tan importante, aquí tienes los puntos clave:

# ¿Para qué sirve?

Las computadoras y servidores en Internet se comunican entre sí utilizando números únicos llamados direcciones IP (por ejemplo, 192.0.2.1). Sin embargo, para los seres humanos es muy difícil recordar una serie de números para cada página web que queremos visitar.

El DNS se encarga de traducir los nombres de dominio que escribimos en el navegador, como google.com o wikipedia.org, a la dirección IP numérica que la computadora entiende.

# ¿Cómo funciona paso a paso?

Cuando escribes una dirección web en tu navegador, ocurre lo siguiente:

- La petición: Escribes ejemplo.com y tu dispositivo pregunta por esa dirección a un servidor DNS, generalmente provisto por tu operador de Internet.

- La búsqueda: Si el servidor no tiene la dirección guardada, consulta a otros servidores en cascada (servidores raíz, servidores de nombres de nivel superior como .com, etc.) hasta encontrar el que tiene la información exacta.

- La respuesta: El servidor DNS localiza la dirección IP (por ejemplo, 93.184.216.34) y se la devuelve a tu navegador.

- La conexión: Tu navegador utiliza esa IP para conectarse al servidor web y mostrarte la página.

# Puntos clave a recordar

- Es automático y rápido: Todo este proceso ocurre en milisegundos, por lo que ni lo notas.

- Tipos de DNS públicos: Aunque tu operador te asigna uno por defecto, existen alternativas populares y gratuitas que suelen ser más rápidas o seguras, como Google (8.8.8.8) o Cloudflare (1.1.1.1).

Para realizar una instalación y configuración completa de un servidor DNS (BIND9) en una máquina virtual de Ubuntu, debes seguir un flujo ordenado que va desde la preparación hasta la prueba final.



SERVIDOR

# 1. Instalar BIND9:

Actualiza los paquetes e instala BIND9 ejecutando en la terminal:
```
sudo apt update && sudo apt install bind9 bind9utils -y
```
Cómo verificar: Ejecuta "sudo systemctl status bind9" y comprueba que el estado sea "active" (running).

# 2. Configurar las opciones globales:

Edita el archivo de opciones para configurar los reenviadores externos (por ejemplo, Cloudflare y Google):
```
sudo nano /etc/bind/named.conf.options
```
Añade o reemplaza el contenido por el siguiente bloque:
```
options {
    directory "/var/cache/bind";
    recursion yes;
    forwarders {
        1.1.1.1;
        8.8.8.8;
    };
    dnssec-validation auto;
    listen-on { any; };
    listen-on-v6 { any; };
};
```
Guarda el archivo (Ctrl + O, Enter) y sal (Ctrl + X).

Cómo verificar: Ejecuta "sudo named-checkconf" sin que devuelva ningún error.

# 3. Definir una zona local (Opcional):

Si deseas crear tu propio dominio local (ej. miservidor.local), edita el archivo de zonas locales:
```
sudo nano /etc/bind/named.conf.local
```
Añade la siguiente estructura:
```
zone "miservidor.local" {
    type master;
    file "/etc/bind/db.miservidor.local";
};
```
Guarda y cierra el archivo.

# 4. Crear el archivo de registro de zona:

Crea y edita el archivo de base de datos para tu dominio local basado en la plantilla por defecto:
```
sudo nano /etc/bind/db.miservidor.local
```
Modifica el contenido para que quede similar a esto (reemplaza 192.168.1.50 por la IP real de tu máquina virtual):
```
@   IN  SOA ns.miservidor.local. admin.miservidor.local. (
              2026100801 ; Serial
              600        ; Refresh
              1800       ; Retry
              604800     ; Expire
              300 )      ; Negative Cache TTL

@   IN  NS  ns.miservidor.local.
@   IN  A   192.168.1.50
ns  IN  A   192.168.1.50
www IN  A   192.168.1.50
```
Cómo verificar: Valida la zona ejecutando "sudo named-checkzone miservidor.local /etc/bind/db.miservidor.local" (debe mostrar OK).

# 5. Reiniciar y aplicar cambios:

Reinicia el servicio BIND9 para aplicar toda la configuración:
```
sudo systemctl restart bind9
```
Cómo verificar: Comprueba que responda a las consultas ejecutando "dig @127.0.0.1 www.miservidor.local" y verificando que devuelva tu dirección IP en la sección de respuesta.



CLIENTE

Para configurar un equipo con Ubuntu como cliente para que utilice tu servidor DNS (el de la máquina virtual), puedes hacerlo de forma gráfica o mediante la línea de comandos (Netplan). Aquí tienes el método más rápido y estándar usando la terminal:

# 1. Identificar la interfaz de red:

Abre la terminal en tu cliente Ubuntu y ejecuta el siguiente comando para ver el nombre de tu conexión de red (por ejemplo, enp0s3 o wlan0):
```
ip route show default | awk '{print $5}'
```
Cómo verificar: El comando devolverá directamente el nombre de tu interfaz activa.

# 2.Editar la configuración de Netplan:

Ubuntu gestiona las redes mediante Netplan. Busca el archivo de configuración en /etc/netplan/ (suele tener un nombre como 01-netcfg.yaml o 50-cloud-init.yaml):
```
sudo nano /etc/netplan/01-netcfg.yaml
```
Cómo verificar: El editor se abrirá mostrando la configuración de red actual.

# 3.Añadir la IP de tu servidor DNS:

Modifica el archivo para agregar la sección nameservers apuntando a la dirección IP de tu servidor DNS virtual (por ejemplo, 192.168.1.50):
```
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true
      nameservers:
        addresses: [192.168.1.50]
```
Guarda los cambios (Ctrl + O, Enter) y sal (Ctrl + X).

# 4.Aplicar los cambios de red:

Aplica la nueva configuración ejecutando:
```
sudo netplan apply
```
Cómo verificar: Ejecuta resolvectl status y comprueba que en la sección de tu interfaz aparezca la IP de tu servidor DNS configurada correctamente.
