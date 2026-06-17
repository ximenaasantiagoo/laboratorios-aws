# Lab: Shell Bash

> ### Objetivo:
> Automatizar copias de seguridad mediante alias y gestionar rutas de ejecución con la variable PATH, asegurando la persistencia de configuraciones en el entorno del sistema para optimizar la administración de software.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.

### Paso 2: Creación del alias para backup
Primero, verifiqué que estuviera en la carpeta principal de mi usuario. Después, creé un atajo rápido (alias) llamado backup usando el comando `tar -cvzf`. Este atajo sirve para juntar y comprimir carpetas en un archivo `.tar.gz`, mostrando en la pantalla la lista de todo lo que se va guardando.

### Paso 3: Ejecución del respaldo de la carpeta CompanyA
Utilicé el alias creado para generar una copia de seguridad de la carpeta CompanyA. El comando tomó el nombre del archivo final (`backup_companyA.tar.gz`) como el primer parámetro y la carpeta de origen como el segundo.

### Paso 4: Verificar la creación del archivo de respaldo
Finalmente, ejecuté el comando de listado para comprobar que el archivo comprimido se hubiera generado correctamente en el directorio actual junto a la carpeta original

### Paso 5: Navegación y ejecución local del script
Me moví a la carpeta bin dentro de CompanyA y ejecuté el script `hello.sh` usando `./` para indicarle al sistema que el archivo estaba en la carpeta actual.

### Paso 6: Intento de ejecución fuera de la carpeta (Error de comando)
Regresé a la carpeta anterior (CompanyA). Intenté ejecutar el script de dos formas: 

- Primero usando su ruta (`./bin/hello.sh`), lo cual funcionó bien
- Luego escribiendo solo su nombre (`hello.sh`), lo que provocó un error del sistema.

### Paso 7: Revisión de la variable `$PATH`
Para entender por qué el sistema no encontraba el script al llamarlo solo por su nombre, revisé el contenido de la variable `$PATH` usando el comando `echo`.

### Paso 8: Actualización del PATH y validación final 
Añadí la ruta de la carpeta bin al final de la variable `$PATH`. Después de hacer esto, volví a intentar ejecutar el script escribiendo únicamente `hello.sh` desde cualquier ubicación, y esta vez el sistema lo reconoció y ejecutó correctamente.


