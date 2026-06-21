# Lab: Scripting del shell Bash

> Objetivo: Crear un directorio 

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso1.1.png?raw=true)

### Paso 2: Creación del script
Dentro de la instancia EC2, usé `nano` para crear el archivo `crear_archivos.sh`. 
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso2.png?raw=true)

El script cuenta cuántos archivos con el patrón `Ximena<número>` ya existen en el directorio usando `find`, y a partir de ese conteo crea el siguiente grupo de 25 archivos vacíos con `touch` dentro de un ciclo `while`, sin tener que escribir los números a mano.
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso2.1.png?raw=true)

### Paso 3: Ejecución del script
Ejecuté el script mandándolo a llamar con `bash crear_archivos.sh`.
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso3.png?raw=true)

### Paso 4: Validación con ls
Para comprobar que el script creó los 25 archivos esperados, usé `ls -l Ximena*`, pero por defecto los ordena alfabéticamente. 
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso4.png?raw=true)

Para odernar los archivos numéricamente en lugar del orden alfabético, ocupé el comando `-v`
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab15/paso4.1.png?raw=true)
