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
