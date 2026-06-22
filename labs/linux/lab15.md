# Lab: Scripting del shell Bash

> ### Objetivo
> Crear un directorio 

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso1.png?raw=true)

### Paso 2: Creación del script
Dentro de la instancia EC2, usé `nano` para crear el archivo `crear_archivos.sh`. 
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso2.png?raw=true)

Este script basándose en la cantidad de archivos existentes con el nombre "Ximena" mediante un ciclo, genera automáticamente los 25 archivos vacíos secuenciales para evitar duplicados.
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso2.1.png?raw=true)

### Paso 3: Ejecución del script
Ejecuté el script mandándolo a llamar con `bash crear_archivos.sh`.
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso3.png?raw=true)

### Paso 4: Validación con ls
Para comprobar que el script creó los 25 archivos, usé el comando `ls -v` para listarlos de manera ordenada 
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso4.png?raw=true)

