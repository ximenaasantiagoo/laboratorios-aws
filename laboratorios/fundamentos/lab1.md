# Lab: Introducción a Amazon EC2

> ### Objetivo
> Gestionar instancias en Amazon Elastic Compute Cloud (Amazon EC2) que es un servicio web que proporciona capacidad de cómputo segura y de tamaño modificable en la nube además permite pagar solo por la capacidad que realmente se utiliza

### Paso 1: Configuración de la Instancia 

En la consola de AWS configuré mi instancia con los siguientes datos
* **Nombre:** Asigné el nombre de `Web Server` para crea una etiqueta de identificación.
* **Sistema Operativo Amazon Machine Image (AMI):** Seleccioné el sistema operativo base del servidor `Amazon Linux 2023` 
* **Tipo de Instancia:** Elegí la capacidad de hardware del servidor, seleccionando `t3.micro` debido a las restricciones del laboratorio.
* **Seguridad:** Omití la asignación de claves de acceso `Proceed without a key pair`, ya que en este laboratorio no fue necesario iniciar sesión directamente en el servidor.
* **Red:**  Asigné la instancia a la red `Lab VPC`, configuré un firewall virtual llamado "Web Server security group" y eliminé la regla Secure Shell (SSH) por defecto con el fin de aumentar la seguridad del servidor.
* **Almacenamiento:** Mantuve el disco virtual de almacenamiento por defecto que son `8 GiB` de tipo Amazon Elastic Block Store (EBS), el cual funcionará como el volumen raíz (de arranque) para el sistema operativo.







### Paso 2: Monitoreo y comprobaciones de estado

Una vez encendida la instancia, revisé que todo funcionara bien:

* Vi las métricas de rendimiento en tiempo real desde `Amazon CloudWatch`
* Confirmé que las pruebas automáticas pasaron correctamente (`2/2 checks passed`), tanto a nivel de hardware como de sistema operativo
* Usé la herramienta `Get Instance Screenshot` para ver el estado visual del servidor sin necesitar abrir una terminal

### 3. Configurar el firewall y habilitar el acceso HTTP

Cuando intenté abrir la `Public IPv4` en el navegador, la página no cargó. El problema era que AWS bloquea todo el tráfico por defecto. Para resolverlo:

* Abrí el `Web Server security group` y edité sus reglas de entrada (`Inbound rules`)
* Agregué una regla que permite tráfico `HTTP` por el puerto `80` desde cualquier origen (`0.0.0.0/0`)

Después de eso, el servidor respondió correctamente en el navegador.

### 4. Escalar los recursos verticalmente

Para simular un ajuste de capacidad, apagué la instancia y le cambié los recursos:

* **Tipo de instancia:** de `t3.micro` a `t3.small`, lo que duplicó la memoria RAM disponible
* **Almacenamiento:** amplié el volumen de `Amazon EBS` de `8 GiB` a `10 GiB`

### 5. Probar la protección contra terminación y apagar el servidor

En la última parte del lab probé el mecanismo que evita borrados accidentales:

* Intenté terminar la instancia y AWS me lo bloqueó gracias a la protección contra terminación que habíamos activado antes
* Desactivé esa protección manualmente desde la configuración de la instancia
* Terminé la instancia y liberé el volumen de almacenamiento asociado

### Conclusión

