# Lab: Administración de software

> ### Objetivo:
> Actualizar los paquetes del sistema operativo Linux mediante el gestor nativo y ejecutar la reversión de software a versiones previas para garantizar la estabilidad del entorno. Asimismo, realizar la instalación y configuración de la interfaz de línea de comandos de AWS (AWS CLI) para habilitar la gestión optimizada de recursos en la nube.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso1.1.png?raw=true)

### Paso 2: Actualización del servidor Linux con Yum
Verifiqué estar en la carpeta correcta (`companyA`) y busqué las actualizaciones disponibles en los repositorios. Después, usé el comando `yum` con permisos de administrador (`sudo`) para instalar los parches de seguridad y actualizar por completo todos los paquetes del sistema. 
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso2.png?raw=true)

Por último, instalé `httpd` para dejar un registro en el historial de actualizaciones.
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso2.1.png?raw=true)

### Paso 3: Reversión de la actualización de un paquete en Yum
Revisé el historial de transacciones de `yum` para identificar el ID de la última actualización del sistema. 
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso3.png?raw=true)
Luego revisé ese movimiento y usé el comando `undo` con permisos de administrador para volver el paquete a su versión anterior y evitar problemas en el sistema.
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso3.1.png?raw=true)

### Paso 4: Instalación y verificación de AWS CLI en Red Hat Linux
Verifiqué las versiones instaladas de `python3` y `pip3` para asegurar la compatibilidad con los requisitos del sistema. 
![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso4.png?raw=true)

Luego, utilicé el comando `curl` para descargar el instalador oficial de AWS CLI en un archivo comprimido. 
![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso4.1.png?raw=true)

Posteriormente lo descomprimí con `unzip` y ejecuté el script de instalación con privilegios de administrador (`sudo`). 
![imagen9](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso4.2.png?raw=true)
![imagen10](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso4.3.png?raw=true)

Finalmente, validé el funcionamiento de la herramienta con el comando `aws help`. 
![imagen11](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso4.4.png?raw=true)
En la ventana de credenciales junto a AWS CLI, seleccione Mostrar para recuperar las credenciales de acceso (`access key` y `secret access key`). 
![imagen12](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso4.5.png?raw=true)

 
### Paso 5: Configuración de AWS CLI y vinculación con la cuenta de AWS
Inicié la configuración de la herramienta con el comando `aws configure`, definiendo la región por defecto como `us-west-2` y el formato de salida en formato json. 
![imagen13](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso5.png?raw=true)

Después, abrí el archivo de configuración con el editor `nano` para registrar manualmente las credenciales de acceso (`access key`, `secret access key` y `session token`) obtenidas en el paso anterior.  
![imagen14](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso5.1.png?raw=true)

Finalmente, accedí a la consola de AWS para copiar el `Instance ID`. 
![imagen15](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso5.2.png?raw=true)

Ejecuté un comando de descripción en la terminal para validar que la interfaz ya tuviera comunicación directa con la instancia.
![imagen16](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab11/paso5.3.png?raw=true)


