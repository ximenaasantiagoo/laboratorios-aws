# Lab: Scripting del shell Bash

> ### Objetivo: 
> Crear un script bash que automatice la copia de seguridad de una carpeta 

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.

### Paso 2: Revisar la ubicación y crear el archivo del script
Confirmé que estaba en la carpeta de inicio correcta usando `pwd`. Después, creé un archivo vacío llamado `backup.sh` y le di permisos con `chmod` para que el sistema me deje ejecutarlo como un programa.

### Paso 3: Escribir el código dentro del script
Abrí el archivo con `vi backup.sh` y con la tecla `i` para poder pegar las líneas de código, el cual devuelve la fecha de hoy, elige dónde guardar el archivo y pone la carpeta CompanyA en un archivo comprimido.

Para salir y guardaar, presioné la tecla `esc`, escribí `:wq` y le di `Enter`

### Paso 4: Guardar la copia de seguridad y revisar que funcione
Escribí `./backup.sh` para iniciar el script. Al final, revisé con `ls backups/` para asegurarme de que la copia de seguridad realmente se hubiera creado con la fecha de hoy.
