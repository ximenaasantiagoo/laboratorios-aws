# Lab: Introducción a Amazon EC2

> ### Objetivo
> Gestionar instancias en Amazon Elastic Compute Cloud (Amazon EC2) que es un servicio web que proporciona capacidad de cómputo segura y de tamaño modificable en la nube, además permite pagar solo por la capacidad que realmente se utiliza

### Paso 1: Configuración Inicial de la Instancia 

En la consola de AWS configuré mi instancia con los siguientes datos:

* **Nombre:** Asigné el nombre de `Web Server` para crea una etiqueta de identificación.
* **Sistema Operativo Amazon Machine Image (AMI):** Seleccioné el sistema operativo base del servidor `Amazon Linux 2023` 
* **Tipo de Instancia:** Elegí la capacidad de hardware del servidor, seleccionando `t3.micro` debido a las restricciones del laboratorio.
* **Seguridad:** Omití la asignación de claves de acceso `Proceed without a key pair`, ya que en este laboratorio no fue necesario iniciar sesión directamente en el servidor.
* **Red:**  Asigné la instancia a la red `Lab VPC`, configuré un firewall virtual llamado "Web Server security group" y eliminé la regla Secure Shell (SSH) por defecto con el fin de aumentar la seguridad del servidor.
* **Almacenamiento:** Mantuve el disco virtual de almacenamiento por defecto que son `8 GiB` de tipo Amazon Elastic Block Store (EBS), el cual funcionará como el volumen raíz (de arranque) para el sistema operativo.
  
![Consola de AWS - Configuración de la Instancia EC2](/imagenes/lab1/paso1.png)

### Paso 2: Configuración de Detalles Avanzados
En la sección de configuraciones avanzadas de la consola, apliqué los siguientes parámetros:
* **Protección contra terminación:** En Advanced details habilité la opción `Termination protection` con el fin de añadir una capa de seguridad para la prevención de eliminación accidental de la instancia.
* **Datos de usuario:** Introduje un script Bash para automatizar la configuración inicial del servidor al arrancar por primera vez; este activa un servidor web Apache y genera una página de inicio básica (index.html) con un mensaje de bienvenida personalizado.


### Paso 3: Lanzamiento de la Instancia
Ejecuté el lanzamiento del servidor con `Launch instance` y revisé su estado hasta que cambiara a `Running` y supere las verificaciones del sistema `2/2 checks passed`, asignándole automáticamente un Domain Name System (DNS) público para su acceso.

### Paso 4: Monitoreo de la Instancia 
Una vez encendida la instancia, revisé que todo funcionara bien:
* Vi las métricas de rendimiento en tiempo real desde `Amazon CloudWatch`
* Confirmé que las pruebas automáticas pasaron correctamente (`2/2 checks passed`), tanto a nivel de hardware como de sistema operativo
* Usé la herramienta `Get Instance Screenshot` para ver el estado visual del servidor sin necesitar abrir una terminal


### Paso 5: Configuración del Grupo de Seguridad y dar acceso al Servidor Web

Cuando intenté abrir la `Public IPv4` en el navegador, la página no cargó. El problema era que AWS bloquea todo el tráfico por defecto entonces para resolverlo realicé lo siguiente:
* Abrí el `Web Server Security Group` y edité sus reglas de entrada (`Inbound rules`)
* Agregué una regla que permite tráfico `HTTP` por el puerto `80` desde cualquier origen.
  
Después de eso, el servidor respondió correctamente en el navegador.

### Paso 6: Cambiar el tamaño de Instancia 
Para simular un ajuste de capacidad, detuve el servidor web hasta que su estado cambió a `stopped`, ya que es un requisito obligatorio para poder modificar el hardware base.

* **Escalamiento de Cómputo:** Modifiqué el tipo de instancia de `t3.micro` a `t3.small` desde el menú de configuración, duplicando la capacidad de memoria RAM disponible para el servidor.
* **Escalamiento de Almacenamiento:** Ingresé a la sección de volúmenes de Amazon EBS y expandí el tamaño del volumen raíz, incrementando el disco virtual de `8 GiB ` a `10 GiB`.

Finalmente volví a encender la instancia (`Start instance`) para aplicar las nuevas capacidades de hardware de manera exitosa.

### Paso 7: Validación de Seguridad y Cierre del Ciclo de Vida
Comprobé el funcionamiento del mecanismo que evita borrados accidentales:
* **Prueba de Eliminación:** Intenté terminar (`Terminate`) la instancia de manera directa y AWS me lo bloqueó gracias a la protección contra terminación que habíamos activado antes
* **Bloqueo de Seguridad:** El sistema rechazó la solicitud mediante un mensaje de error en la consola, validando que la protección contra terminación se encontraba activa y previno un borrado accidental.
* **Desactivación y Limpieza:** Modifiqué los atributos de la instancia para deshabilitar la protección y procedí a terminar el servidor de forma definitiva.
  


