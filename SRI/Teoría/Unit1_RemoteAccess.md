Configuración de acceso SSH sin contraseña desde Windows a Ubuntu

1. Comprobar la carpeta SSH en Windows. En Windows PowerShell:
```
dir $env:USERPROFILE\.ssh
```
Crear una clave SSH en Windows
Ejecutar:
```
ssh-keygen -t ed25519
```
Cuando aparezcan las siguientes preguntas, pulsar Enter en todas:

Enter file in which to save the key:
Enter passphrase:
Enter same passphrase again:
Se crearán:

id_ed25519
id_ed25519.pub
Comprobarlo con:

dir $env:USERPROFILE\.ssh
Mostrar la clave pública
En PowerShell:

type $env:USERPROFILE\.ssh\id_ed25519.pub
Copiar toda la línea que aparece, que empieza por:

ssh-ed25519
Conectarse al servidor Ubuntu
Desde PowerShell:

ssh raul@172.16.5.140
Introducir la contraseña del usuario raul.

Crear la carpeta SSH en Ubuntu En el servidor Ubuntu:
mkdir -p ~/.ssh
Dar permisos:

chmod 700 ~/.ssh
Crear el archivo de claves autorizadas
Ejecutar:

nano ~/.ssh/authorized_keys
Pegar dentro la clave pública copiada desde Windows.

Guardar:

Ctrl + O → Enter

Salir:

Ctrl + X
Dar permisos al archivo
En Ubuntu:

chmod 600 ~/.ssh/authorized_keys
Y:

chown -R $USER:$USER ~/.ssh
Reiniciar el servicio SSH
Ejecutar:

sudo systemctl restart ssh
Introducir la contraseña de Ubuntu cuando la solicite.

Comprobar que la clave se ha guardado
Ejecutar:

cat ~/.ssh/authorized_keys
Debe aparecer la clave:

ssh-ed25519 AAAA... asir2@DESKTOP-68H721U
Salir del servidor
exit
Comprobar el acceso sin contraseña
Desde Windows PowerShell:

ssh raul@172.16.5.140
Si todo está correctamente configurado, se entra directamente al servidor:

raul@raul-VirtualBox:~$
sin introducir la contraseña del usuario raul.
