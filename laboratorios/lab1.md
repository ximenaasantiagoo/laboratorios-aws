# <span style="color: #f3b4dd !important;">Lab: Introducción a Amazon EC2</span>


>  `Amazon EC2` `Máquina Virtual` `AWS`

---
### Objetivo

En este laboratorio aprendí a gestionar instancias en Amazon EC2. Practiqué cómo lanzar una máquina virtual, protegerla con Security Groups, monitorear su estado, cambiar sus recursos de cómputo y almacenamiento, y configurar la protección contra terminación para evitar borrados accidentales.

### 1. Lanzar la Instancia EC2

Desde la consola de AWS configuré mi primera instancia con estos datos:

* **Nombre:** `Web Server`
* **Sistema Operativo (AMI):** `Amazon Linux 2023`
* **Tipo de Instancia:** `t3.micro` (2 vCPU, 1 GiB de RAM)
* **Seguridad:** Sin par de llaves (`Key pair`) porque no necesitaba acceso por SSH
* **Red:** Dentro de la `Lab VPC`

### 2. Monitoreo y comprobaciones de estado

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

