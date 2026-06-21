# Lab: Administración de archivos de registro

> ### Objetivo:
> Revisar el último registro y las salidas de registro seguro de la máquina Linux

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab12/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab12/paso1.1.png?raw=true)

### Paso 2: Revisión de registros de seguridad y autenticación (Secure Logs)
Primero, verifiqué que estuveiera en el directorio correcto (`companyA`) y revisé el archivo de registro de seguridad para visualizar los intentos de autenticación en el sistema 
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab12/paso2.png?raw=true)

Este archivo permite identificar auditorías de acceso, mostrando las direcciones IP de origen, los puertos utilizados y si las credenciales fallaron o fueron aceptadas. Para salir de la visualización del archivo, presioné la tecla `q`.
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab12/paso2.1.png?raw=true)

### Paso 3: Inspección del historial de accesos con lastlog
Finalmente para verificar la última fecha y hora de inicio de sesión de todos los usuarios registrados en el sistema, ejecuté la herramienta nativa de Linux `lastlog`.
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab12/paso3.png?raw=true)

