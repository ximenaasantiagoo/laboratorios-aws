# Lab: Creación de una VPC y lanzamiento de un servidor web

> Objetivo: Crear una red personalizada (VPC) desde cero con subredes públicas y privadas en distintas Zonas de Disponibilidad, configurar un Security Group como firewall y lanzar un servidor web Apache automático dentro de una instancia EC2.

### Paso 1: Crear la VPC base con el Asistente de AWS
Para empezar el proyecto de nuestro cliente, entré a la consola de AWS y busqué el servicio VPC. Usé la opción de "VPC and more" para que el asistente me ayudara a crear la estructura inicial (VPC, un Internet Gateway, un NAT Gateway y las dos primeras subredes). Configuré los datos principales de la red de la siguiente manera:
- IPv4 CIDR: `10.0.0.0/16` 
- Zonas de Disponibilidad (AZs): Seleccioné 1 para el inicio.
- Subredes: Configuré 1 pública `(10.0.0.0/24)`y 1 privada `(10.0.1.0/24)`.
- NAT Gateway: Seleccioné que se creara en 1 Zona de Disponibilidad para darle salida a internet de forma segura a la subred privada.
Nombres para la vista previa:
- VPC: Lab VPC
- Subredes: Public Subnet 1 y Private Subnet 1
- Tablas de ruteo: Public Route Table y Private Route Table

### Paso 2: Crear subredes adicionales para Alta Disponibilidad
Para asegurar que la arquitectura de nuestro cliente sea tolerante a fallos, creé dos subredes extra en una segunda Zona de Disponibilidad. 
- Segunda Subred Pública:
    - VPC: Lab VPC
    - Nombre: Public Subnet 2
    - Bloque CIDR: `10.0.2.0/24` 
- Segunda Subred Privada:
    - VPC: Lab VPC
    - Nombre: Private Subnet 2
    - Bloque CIDR: `10.0.3.0/24` 

### Paso 3: Asociar las nuevas subredes a las Tablas de Ruteo
Como creé las subredes de forma manual en el paso anterior, AWS no sabe automáticamente cuáles son públicas y cuáles privadas. Tuve que ir a `Route Tables` para unirlas con su respectivo camino:


Con esto, mi red ya quedó bien distribuida con dos subredes públicas y dos privadas repartidas en dos zonas distintas.

### Paso 4: Configurar el Firewall Virtual (Web Security Group)
Antes de lanzar el servidor, creé la regla de seguridad que actuará como firewall para protegerlo. Fui a Security Groups y creé uno nuevo con los siguientes datos:
- Nombre: Web Security Group
- Descripción: Enable HTTP access
- VPC asociada: Lab VPC

En las reglas de entrada, agregué una nueva regla para que el servidor pueda recibir visitas:
- Tipo: `HTTP` (Abre automáticamente el puerto 80).
- Origen (Source): `Anywhere IPv4 (0.0.0.0/0)`, para que cualquier persona en internet pueda cargar la página web.

### Paso 5: Lanzar el Servidor Web con User Data automático
Finalmente, fui al servicio de EC2 para levantar la instancia que tendrá el sitio web. Le dí a Launch instances y configuré lo siguiente:
- Nombre: Web Server 1
- Sistema Operativo: `Amazon Linux 2 AMI`.
- Tipo de instancia: `t3.micro` con la llave de acceso `vockey`.
- Configuración de Red: Seleccioné `Lab VPC`.
    - Ubiqué la instancia dentro de la subred pública que creé manualmente: `Public Subnet 2`.
    - Activé la opción Auto-assign public IP (en Enable) para que tuviera una dirección pública en internet.
    - En Firewall, seleccioné mi grupo existente: `Web Security Group`.

Para evitar instalar todo a mano después de encenderla, fui a Advanced details y pegué el siguiente script en la sección de User data. Esto automatiza la instalación de Apache, PHP, descarga la aplicación del cliente desde un bucket de S3 y enciende el servicio web: 
#!/bin/bash

Instalar el servidor web Apache, MySQL y PHP
`yum install -y httpd mysql php`

Descargar los archivos del laboratorio del cliente
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RESTRT-1/267-lab-NF-build-vpc-web-server/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/

Configurar Apache para que prenda automáticamente y arrancar el servicio
`chkconfig httpd on`
`service httpd start`


### Paso 6: Prueba final en el navegador
Para comprobar que toda la infraestructura de red y el servidor estuvieran bien, seleccioné mi instancia Web Server 1, fui a la pestaña de Details y copié la dirección de Public IPv4 DNS. 

Abrí una pestaña nueva en mi navegador, pegué la dirección y le dí Enter. El sitio web cargó con éxito mostrando la página personalizada del cliente, confirmando que la VPC y el ruteo funcionan de diez.  
