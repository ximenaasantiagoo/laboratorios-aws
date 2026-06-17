# Lab: Administración de software

> ### Objetivo:
> Actualizar los paquetes del sistema operativo Linux mediante el gestor nativo y ejecutar la reversión de software a versiones previas para garantizar la estabilidad del entorno. Asimismo, realizar la instalación y configuración de la interfaz de línea de comandos de AWS (AWS CLI) para habilitar la gestión optimizada de recursos en la nube.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso1.1.png?raw=true)

### Paso 2: Actualización del servidor Linux con Yum
Verifiqué estar en la carpeta correcta (`companyA`) y busqué las actualizaciones disponibles en los repositorios. Después, usé el comando `yum` con permisos de administrador (`sudo`) para instalar los parches de seguridad y actualizar por completo todos los paquetes del sistema. Por último, instalé `httpd` para dejar un registro en el historial de actualizaciones.

### Paso 3: Reversión de la actualización de un paquete en Yum
Revisé el historial de transacciones de `yum` para identificar el ID de la última actualización del sistema. 

Luego, consulté el detalle de ese movimiento específico y utilicé el comando `undo` con privilegios de administrador para deshacer los cambios, revirtiendo el paquete a su versión anterior para asegurar la estabilidad del entorno.



### Paso 4: Instalación y verificación de AWS CLI en Red Hat Linux
Verifiqué las versiones instaladas de `python3` y `pip3` para asegurar la compatibilidad con los requisitos del sistema. 


Luego, utilicé el comando `curl` para descargar el instalador oficial de AWS CLI en un archivo comprimido, lo descomprimí con `unzip` y ejecuté el script de instalación con privilegios de administrador (`sudo`). 

Finalmente, validé el funcionamiento de la herramienta con el comando `aws help`. En la ventana de credenciales junto a AWS CLI, seleccione Mostrar para recuperar las credenciales de acceso (`access key` y `secret access key`). Copie y pegue estas dos claves en un editor de texto para usarlas posteriormente. 

### Paso 5: Configuración de AWS CLI y vinculación con la cuenta de AWS
Inicié la configuración de la herramienta con el comando `aws configure`, definiendo la región por defecto como `us-west-2` y el formato de salida en formato json. 

Después, abrí el archivo de configuración con el editor `nano` para registrar manualmente las credenciales de acceso (`access key`, `secret access key` y `session token`) obtenidas en el paso anterior. 

Finalmente, accedí a la consola de AWS para copiar el `Instance ID` del servidor *Command Host* y ejecuté un comando de descripción en la terminal para validar que la interfaz de línea de comandos ya tenía comunicación directa con la instancia.

