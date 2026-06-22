# Lab: Creación de subredes en una VPC

> ### Objetivo 
> Familiarizarse con la consola de AWS para diseñar y configurar una Amazon VPC con sus respectivas subnets e IP.

### Paso 1: Buscar el servicio en la consola
Dentro de la consola de AWS, en la barra de búsqueda, escribí VPC y la seleccioné para abrir el panel de control del servicio.

### Paso 2: Iniciar el asistente
Utilicé Launch VPC Wizard (Asistente para lanzar VPC), lo que me permitió configurar todo de forma guiada.

### Paso 3: Elegir la configuración de red
Seleccioné la opción VPC with a Single Public Subnet (VPC con una sola subred pública). Elegí esta opción porque el cliente necesita que sus recursos se conecten a internet.

### Paso 4: Configurar los datos de la VPC y la Subnet
Borré los datos que venían por defecto y rellené el formulario con los siguientes datos (calculados para cubrir las 15,000 IPs que pide el cliente):
- VPC Name: First VPC
- IPv4 CIDR block (Para la VPC): 192.168.0.0/18     
- IPv6 CIDR block: Lo dejé en No IPv6.
- Subnet name: Public subnet
- Public subnet's IPv4 CIDR: 192.168.1.0/26 (Suficiente para alojar al menos 50 IPs públicas).
- Availability Zone: Seleccioné No Preference.
Los demás valores los dejé como venían por defecto

### Paso 5: Crear y verificar
Hice clic en Create VPC en la esquina inferior derecha. Al ver el mensaje de éxito, fui al menú de la izquierda, seleccioné Your VPCs y verifiqué que mi nueva red ya aparecía activa en la lista.


