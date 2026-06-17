
# Lab: Servicios Administrativos 

> ### Objetivo:
> Verificar el correcto funcionamiento y disponibilidad del servidor web mediante la comprobación de su estado y la validación de conexiones HTTP locales. Asimismo, implementar el monitoreo de rendimiento de la instancia Amazon Linux 2 EC2, utilizando la herramienta nativa top de Linux y métricas de AWS CloudWatch para asegurar la optimización de los recursos.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso1.png?raw=true)
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso1.1.png?raw=true)

### Paso 2: Verificar el estado del servicio httpd
Primero, comprobé el estado del servicio `httpd` para validar si se encontraba en ejecución dentro del sistema
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso2.png?raw=true)
Al ejecutarlo, la terminal indicó que el servicio estaba instalado y listo (loaded), pero con un estado inactive (dead), lo que significa que el servidor web no estaba corriendo en ese momento. Para iniciar el servicio, ejecuté el comando de arranque
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso2.1.png?raw=true)
Posteriormente, volví a verificar el estado para confirmar que el cambio se hubiera aplicado correctamente
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso2.2.png?raw=true)

### Paso 3: Validación de conectividad HTTP y detención del servicio
Con el servidor en ejecución, abrí una nueva pestaña en el navegador web e ingresé la dirección IP pública de la instancia utilizando el protocolo HTTP, esto con el fin de validar su funcionamiento.
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso3.png?raw=true)
Luego detuve el servidor web
![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso3.1.png?raw=true)

### Paso 4: Monitoreo local de procesos 
Para iniciar con la etapa de monitoreo de la instancia, ejecuté el comando `top` en la terminal con el objetivo de visualizar en tiempo real la lista de procesos activos y el consumo de recursos del sistema
![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso4.png?raw=true)
Posteriormente, presioné la tecla `q` para salir de la herramienta interactiva y regresar a la línea de comandos.

### Paso 5: Simulación de carga en la CPU y análisis en tiempo real
Con el fin de evaluar el comportamiento del servidor bajo un entorno de alta exigencia, simulé una carga de trabajo pesada en la instancia EC2. Corrí el script en segundo plano y abrí inmediatamente la herramienta de monitoreo local
![imagen9](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso5.png?raw=true)


### Paso 6: Monitoreo centralizado en AWS CloudWatch
Una vez generada la carga de trabajo, procedí a analizar el impacto en las métricas globales desde la infraestructura de AWS. En la consola de administración, busqué el servicio CloudWatch y accedí a él.

En el panel de navegación izquierdo, seleccioné Dashboards y posteriormente ingresé a Automatic Dashboards. Dentro de la lista, seleccioné la opción de EC2 para desplegar el tablero métrico de la instancia. 
![imagen10](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso6.png?raw=true)

Posteriormente esperé 5 minutos, actualicé el panel y observé la gráfica de utilización de la CPU.
![imagen11](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/linux/lab10/paso6.1.png?raw=true)
