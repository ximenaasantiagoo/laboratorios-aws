# Lab: Trabajo con archivos

> ### Objetivo:
> Adquirir las habilidades necesarias para crear un script o flujo de trabajo básico de SysAdmin (Administrador de Sistemas) mediante respaldos organizados y documentados.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada (labsuser.pem) y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave con `chmod 400` y me conecté al servidor ejecutando `ssh -i labsuser.pem ec2-user@<IP_Pública>`, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab7/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab7/paso1.1.png?raw=true)
### Paso 2: Creación del respaldo con tar
  * Confirmé mi ubicación en `/home/ec2-user` con el comando `pwd`
  * Verifiqué la estructura interna del directorio mediante `ls -R CompanyA`.
    ![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab7/paso2.png?raw=true)
  * Una vez validada la existencia de los archivos, ejecuté `tar -csvpzf backup.CompanyA.tar.gz CompanyA` para empaquetar y comprimir recursivamente toda la carpeta. 
  * Finalmente, utilicé `ls` para comprobar que el archivo comprimido se había generado correctamente en el directorio actual, listo para ser transferido.
    ![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab7/paso2.1.png?raw=true)
### Paso 3: Registro y documentación del respaldo (Logging)
  * Me dirigí a la carpeta del proyecto con `cd /home/ec2-user/CompanyA` y creé un archivo de registro vacío usando `touch SharedFolders/backups.csv`. 
  * Después, inserté la fecha, hora y nombre del archivo de respaldo, visualizando la salida en la terminal al mismo tiempo que se escribía en el documento. 
  * Por último, ejecuté `cat SharedFolders/backups.csv` para verificar que los datos del log se guardaron correctamente.
    ![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab7/paso3.png?raw=true)
### Paso 4: Transferencia del archivo de respaldo
  * Validé con `pwd` que seguía dentro de la carpeta `CompanyA`.
  * Después, utilicé el comando `mv ../backup.CompanyA.tar.gz IA/` para mover el archivo comprimido desde el directorio superior hacia la carpeta del equipo de IA.
  * Finalmente, ejecuté `ls . IA` para listar el contenido de ambos directorios en simultáneo, confirmando que el respaldo ya no estaba en la ruta original y se había transferido correctamente a su destino.
    ![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab7/paso4.png?raw=true)
