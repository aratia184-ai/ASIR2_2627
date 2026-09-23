Las formas posibles de conectarse a la red en una virtual box son:

NAT --> Asigna una IP de forma automática y accede a Internet utilizando la conexión del equipo anfitrión.

Adaptador puente --> La máquina virtual se conecta directamente a la red física a través del adaptador de red del equipo anfitrión.

Red interna --> Permite la comunicación entre varias máquinas virtuales conectadas a la misma red interna. Las máquinas virtuales pueden comunicarse entre sí, pero no tienen acceso directo al equipo anfitrión ni a Internet.

Adaptador solo anfitrión --> Crea una red privada entre el equipo anfitrión y las máquinas virtuales. Las máquinas virtuales pueden comunicarse con el anfitrión y entre ellas, pero no tienen acceso a Internet, salvo que se configure de forma adicional.

Controlador genérico --> Permite utilizar un controlador de red genérico proporcionado por VirtualBox. Se utiliza principalmente para configuraciones o tecnologías de red específicas que requieren un controlador especial.

Red NAT --> Permite conectar varias máquinas virtuales a una misma red NAT. Las máquinas virtuales pueden comunicarse entre sí y acceder a Internet mediante la conexión del anfitrión, mientras que desde la red externa no se puede acceder directamente a ellas salvo que se configuren reglas de redirección de puertos.

Red en la nube --> Permite conectar la máquina virtual a una red basada en servicios de nube compatibles con VirtualBox. Está destinada a configuraciones de infraestructura en la nube y, dependiendo de la versión de VirtualBox y del proveedor, puede tener características experimentales.
