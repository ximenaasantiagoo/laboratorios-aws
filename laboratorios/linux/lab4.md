# Lab: Usuarios y grupos 
> ### Objetivo:
> Implementar la gestión de accesos en AWS mediante la creación de usuarios y grupos de IAM, configurando credenciales iniciales y validando los flujos de autenticación al iniciar sesión con cada una de las identidades configuradas.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada (labsuser.pem) y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave con `chmod 400` y me conecté al servidor ejecutando `ssh -i labsuser.pem ec2-user@<IP_Pública>`, aceptando la autenticidad del host en el primer acceso.

![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso1.1.png?raw=true)

### Pase 2: Creación de Usuarios Locales 
  * Antes de comenzar, validé que estuviera en el directorio home del usuario actual ejecutando el comando `pwd`
  * Para registrar al primer usuario (arosalez) y configurar su credencial de acceso inicial, ejecuté secuencialmente los comandos `useradd` y `passwd` con privilegios de superusuario
    ![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso2.png?raw=true)
  * Verifiqué que el usuario se había integrado correctamente al sistema, ejecuté una lectura del archivo `/etc/passwd` aplicando un filtro con `cut` para mostrar únicamente la primera columna correspondiente a los       nombres de usuario
    _**Nota:** Al introducir la contraseña por defecto (`P@ssword1234!`), el sistema no muestra caracteres ni asteriscos en la pantalla._

![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso2.1.png?raw=true)
### Paso 3: Alta de los usuarios restantes
Repitiendo la estructura de los comandos anteriores (`sudo useradd` y `sudo passwd`), completé el registro individual en el servidor para el resto del personal requerido:
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso3.png?raw=true)
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso3.1.png?raw=true)

### Paso 4: Confirmación del entorno
Una vez concluida la configuración de todo el personal, ejecuté nuevamente la consulta filtrada del archivo de usuarios para asegurar que ninguna identidad faltara.
![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso4.png?raw=true)

### Paso 5: Creación de grupos en el sistema
Para organizar a los usuarios según sus departamentos y roles dentro de la organización, los agrupé por su rol de trabajo utilizando el comando `groupadd`. Primero, creé el grupo de ventas para inicializar el flujo, posteriormente, completé el registro del resto de los departamentos requeridos ejecutando el comando para cada uno de ellos
![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso5.png?raw=true)
![imagen9](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso5.1.png?raw=true)

### Paso 6: Verificación de los grupos creados
Para validar que el sistema operativo registró correctamente los nuevos grupos, realicé una lectura del archivo `/etc/group`
![imagen10](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso6.png?raw=true)
![imagen11](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso6.1.png?raw=true)

### Paso 7: Asignación de usuarios a sus respectivos grupos
Con los grupos listos, utilicé el comando `usermod` con `-a -G` para estructurar los accesos basados en el rol de cada empleado.
![imagen12](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso7.1.png?raw=true)

### Paso 8: Inclusión del usuario administrador (ec2-user)
Como medida de control y supervisión del laboratorio, añadí al usuario por defecto del sistema (`ec2-user`) a absolutamente todos los grupos creados
![imagen13](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso8.png?raw=true)

### Paso 9: Validación final de los grupos
Para validar que cada usuario estuviera dentro del sector correspondiente, ejecuté una última consulta completa al archivo de configuración de grupos
![imagen14](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso9.png?raw=true) 
![imagen15](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso9.1.png?raw=true)

### Paso 10: Cambio de identidad a un usuario nuevo
  * Para validar el comportamiento del entorno y los permisos de las nuevas cuentas, inicié sesión como el usuario `arosalez` utilizando el comando `su` (switch user)
  * Al cambiar de identidad, la terminal se actualizó mostrando la estructura `[arosalez@ec2-user]$`. El indicador final confirmó que seguía posicionada dentro del directorio home del usuario administrador original,     lo cual verifiqué ejecutando `pwd`
    ![imagen16](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso10.png?raw=true)

### Paso 11: Prueba de restricciones de escritura y denegación de permisos
Intenté crear un archivo vacío llamado `myFile.txt` dentro de este directorio, empleando el comando `touch`. El sistema operativo bloqueó la acción debido a que el usuario `arosalez` no cuenta con permisos de escritura sobre la carpeta personal de `ec2-user`.
![imagen17](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso11.png?raw=true)

### Paso 12: Intento como administrador  (Sudoers)
Intenté forzar la creación del archivo elevando privilegios mediante el comando `sudo`. Tras ingresar nuevamente la contraseña de la cuenta para confirmar la identidad, la terminal arrojó el siguiente aviso de seguridad. El comando falló porque `arosalez` no forma parte del archivo de configuración de sudoers (usuarios autorizados con privilegios raíz), lo que provocó que el sistema operativo bloqueara la instrucción y generara una alerta interna.
![imagen18](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso12.png?raw=true)

### Paso 13: Visualización de bitácoras (Logs) 
Regresé a la sesión del usuario administrador original ejecutando `exit`. Una vez de vuelta como `ec2-user`, usé privilegios de superusuario para revisar las últimas líneas del archivo de seguridad (`/var/log/secure`) y verificar cómo el sistema registró el intento fallido de `arosalez`.
![imagen19](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso13.png?raw=true)
![imagen19](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/imagenes/linux/lab4/paso13.1.png?raw=true)

