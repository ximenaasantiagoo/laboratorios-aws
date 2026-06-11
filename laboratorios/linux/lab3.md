# Lab: Línea de comandos Linux

> ### Objetivo:
> Aprender a inspeccionar el sistema, gestionar la sesión activa y buscar o ejecutar comandos anteriores en la terminal Bash.

### Paso 1:Conectarse a la instancia EC2 de Amazon Linux mediante SSH (Mac/Linux)
Para obtener las claves de acceso, descargué el archivo de la llave privada seleccionando el botón Download PEM (se guardó como labsuser.pem). Posteriormente copié y guardé la dirección PublicIP que aparece en ese mismo panel. Cerré el panel de detalles haciendo clic en la `X`. 

### Paso 2: Localización de la clave en la terminal
En la terminal me dirigí a la carpeta donde se descargó el archivo `.pem` utilizando el comando de cambio de directorio. Como el archivo se guardó en la carpeta de Descargas, ejecuté lo siguiente:

### Paso 3: Configuración de seguridad de la clave (chmod)
Modifiqué los permisos del archivo de la llave privada para restringir su acceso y configurarlo como solo lectura, cumpliendo así con los requisitos de seguridad de SSH. Para esto, ejecuté el siguiente comando:

### Paso 4: Ejecución del enlace SSH y acceso al servidor
Inicié la conexión hacia la instancia ejecutando el comando `ssh` e ingresando la dirección IP pública que había copiado previamente. Al ser la primera conexión, la terminal solicitó confirmar la autenticidad del host
### Paso 5: Ejecución de comandos de reconocimiento del sistema y reconocimiento de la sesión
Utilicé la función de autocompletado de la terminal escribiendo `whoa` y presionando la tecla `Tab`, la cual completó automáticamente el comando a `whoami`; al presionar `Enter`, visualicé mi nombre de usuario actual. Posteriormente, ejecuté los comandos `hostname -s` para obtener una versión simplificada del nombre del host del servidor, y `uptime -p` para verificar el tiempo que la instancia llevaba encendida en un formato legible

### Paso 6: Consulta de usuarios activos, zonas horarias, calendarios e identidad
* **Usuarios activos:** Ejecuté el comando `who -H -a` para desplegar un informe detallado sobre los usuarios que han iniciado sesión en el sistema junto con información adicional de la sesión.
* **Zonas horarias:** Para verificar la fecha y hora en diferentes ubicaciones geográficas sin cambiar la configuración global del servidor, utilicé la variable de entorno `TZ` antes del comando `date` para Nueva York y Los Ángeles
* **Calendarios:** Consulté el calendario en formato Juliano (donde los días corren de forma consecutiva del 1 al 365 en lugar de reiniciar cada mes) ejecutando `cal -j`, y exploré vistas alternativas del calendario con los comandos `cal -s` (inicio de semana en domingo) y `cal -m` (inicio de semana en lunes).
* **Identidad:** Ingresé el comando `id ec2-user` para visualizar los identificadores únicos de usuario (UID), de grupo (GID) y los grupos a los que pertenece mi usuario actual en el sistema.

