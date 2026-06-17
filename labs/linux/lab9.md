# Lab: Administración de procesos

> ### Objetivo:
> Monitorear el rendimiento del sistema en tiempo real y automatizar tareas rutinarias, generar reportes de procesos activos y programar su ejecución diaria mediante tareas repetitivas en el servidor.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada (labsuser.pem) y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave con `chmod 400` y me conecté al servidor ejecutando `ssh -i labsuser.pem ec2-user@<IP_Pública>`, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso1.1.png?raw=true)

### Paso 2: Creación y filtrado de la lista de procesos
- Confirmé mi ubicación en `companyA` con `pwd`.
- Luego, ejecuté el comando `sudo ps -aux | grep -v root | sudo tee SharedFolders/processes.csv` para listar todos los procesos activos del sistema, omitiendo aquellos pertenecientes al usuario raiz y guardando el resultado directamente en un nuevo archivo.
    ![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso2.png?raw=true)
- Posteriormente, validé que la información se hubiera registrado correctamente corriendo el comando `cat SharedFolders/processes.csv`.
    ![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso2.1.png?raw=true)

### Paso 3: Monitoreo del sistema en tiempo real (top)
- Ejecuté el comando `top` en la terminal para analizar el rendimiento del sistema y visualizar la lista dinámica de procesos y hilos activos. Durante la inspección, observé en la segunda línea el estado de las tareas, así como el consumo de CPU y memoria.
    ![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso3.png?raw=true)
- Por último, presioné la tecla `q` para salir del monitor y utilicé `top -hv` para consultar las opciones de uso y la versión de la herramienta.
    ![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso3.1.png?raw=true)

### Paso 4: Automatización de tareas con un Cron Job
- Confirmé mi ubicación con `pwd` y abrí el editor de tareas programadas ejecutando `sudo crontab -e`.
- Dentro del archivo, configuré las variables del entorno (`SHELL`, `PATH`, `MAILTO`) y programé una tarea horaria (`0 * * * *`) que busca archivos `.csv`, enmascara sus nombres reemplazando caracteres por `#####` usando `sed`, y redirige el reporte a `filteredAudit.csv`.
    ![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso4.png?raw=true)
- Finalmente, guardé los cambios con `:wq` y validé que el cron job se hubiera instalado correctamente con el comando `sudo crontab -l`. 
    ![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab9/paso4.1.png?raw=true)

