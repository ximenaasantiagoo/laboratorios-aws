# Lab: Trabajo con comandos

> ### Objetivo:
> Ordenar, recortar y modificar el contenido de archivos de texto directamente desde la terminal. Utilizando comandos clave de Linux como tee, sort, cut y sed, conectando sus resultados de forma automática mediante el uso de pipes.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso1.1.png?raw=true)

### Paso 2: Validación de directorio y uso del comando tee
Primero, verifiqué mi ubicación actual en el servidor para asegurarme de estar en el directorio base del usuario. Después, usé el comando `hostname | tee file1.txt` para obtener el nombre del servidor, el comando `tee` funcionó para mostrar el nombre en la pantalla y guardarlo al mismo tiempo en un archivo nuevo. 
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso2.png?raw=true)

Posteriormente, revisé que el archivo se hubiera creado correctamente usando `ls`. 
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso2.1.png?raw=true)

### Paso 3: Uso del comando sort y el operador pipe 
Validé nuevamente mi ubicación con `pwd` y luego creé un archivo de datos llamado `test.csv` para realizar pruebas de ordenamiento y filtrado. Para crear el archivo de forma rápida, utilicé `cat > test.csv`, escribí las líneas correspondientes y guardé el contenido presionando `CTRL+D`. Después, verifiqué que el archivo estuviera listo con `ls`. 
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso3.png?raw=true)

Para organizar la información, ejecuté el comando de ordenamiento `sort` sin ninguna regla adicional entonces el sistema ordenó la lista de forma automática, es decir de forma alfabética y luego por número.
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso3.1.png?raw=true)

Finalmente, utilicé un pipe junto con `grep` para buscar específicamente la fábrica de París dentro del archivo
![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso3.2..png?raw=true)

### Paso 4: Extracción de columnas con el comando cut
Validé mi ubicación en la carpeta base y creé un nuevo archivo llamado `cities.csv` para aprender a separar información por columnas utilizando comas como divisiones. 
![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso4.png?raw=true)

Una vez creado el archivo, utilicé el comando `cut` para recortar el texto y quedarme únicamente con la primera sección de cada línea
![imagen9](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab13/paso4.1.png?raw=true)




