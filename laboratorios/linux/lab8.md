# Lab: Administración de permisos de archivos

> ### Objetivo:
> Administrar la seguridad del sistema de archivos de una empresa, asegurando que la información confidencial esté protegida contra accesos no autorizados o modificaciones accidentales por parte de otros usuarios o departamentos.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada (labsuser.pem) y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave con `chmod 400` y me conecté al servidor ejecutando `ssh -i labsuser.pem ec2-user@<IP_Pública>`, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso1.1.png?raw=true)
### Paso 2: Cambio de propietario y grupo (chown)
  * Validé mi ubicación en `companyA` con `pwd`. 
  * Después, utilicé el comando `sudo chown -R mjackson:Personnel /home/ec2-user/companyA` para asignar recursivamente la estructura completa al CEO y al grupo Personnel.
  * De la misma manera, ajusté las áreas específicas asignando la carpeta `HR` al usuario `ljuan` con su grupo `HR`, y la subcarpeta `HR/Finance` al gerente financiero `mmajor` con su grupo correspondiente.
  * Finalmente, ejecuté `ls -laR` para verificar de forma recursiva que todos los nuevos propietarios y grupos se aplicaron correctamente.
    ![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso2.png?raw=true)
    ![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso2.1.png?raw=true)
### Paso 3: Cambio de modos de permisos (chmod)
  * Nuevamente validé mi ubicación en `companyA` con `pwd`
  * Luego, creé el archivo `symbolic_mode_file` usando `sudo vi` y lo guardé con `:wq`, a este le apliqué el modo simbólico con `sudo chmod g+w` para otorgar permisos de escritura al grupo.
    ![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso3.png?raw=true)
  * Repetí el proceso para crear un segundo archivo llamado `absolute_mode_file`, pero esta vez utilicé el modo absoluto ejecutando `sudo chmod 764` para asignar permisos específicos a usuario, grupo y otros mediante números.
  * Al final, verifiqué ambos cambios ejecutando `ls -l` para comprobar que las nomenclaturas de lectura, escritura y ejecución coincidieran con lo configurado.
    ![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso3.1.png?raw=true)
### Paso 4: Asignación y verificación de permisos por grupo 
  * Aseguré mi posición en `companyA` con `pwd`
  * Después, configuré los propietarios y grupos correspondientes para las nuevas áreas ejecutando `sudo chown -R eowusu:Shipping Shipping` para el departamento de envíos, y `sudo chown -R nwolf:Sales Sales` para el de ventas.
  * Finalmente, validé que la estructura interna y los privilegios asignados fueran correctos ejecutando los comandos `ls -laR Shipping` y `ls -laR Sales` de manera individual.
    ![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab8/paso4.png?raw=true)
