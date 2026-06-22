# Lab: Recursos de redes para una VPC

> ### Objetivo 
> Configurar una red enrutable en AWS (VPC, IGW, tablas de ruteo, SG, NACL y EC2) y solucionar problemas de conectividad.

### Paso 1: Crear una VPC 
Dentro de la consola de AWS, busco y selecciono VPC. Creo la VPC con las siguientes caraterísticas: 
- Nombre: `Test VPC`
- IPv4 CIDR block: `192.168.0.0/18`
Las demás opciones las dejé como están por defecto. 

### Pasos 2: Crear una Subred 
En el menú de la izquierda seleccioné `Subnets`, hago clic en el botón `Create subnet` y configuro los datos de la subred.

### Paso 3: Crear y configurar la Route Table
En el menú de la izquierda seleccioné `Route Tables`, hice clic en el botón `Create route table` y la configuro.

### Paso 4: Crear puerta de enlace de Internet y conectar puerta de enlace
En el panel de navegación izquierdo, seleccioné `Puertas de enlace de Internet`. Cree una puerta de enlace de Internet (`IGW`) y la configuré 


Una vez creado, conecté la puerta de enlace de Internet a la VPC. 


### Paso 5: Configurar rutas y asociar la subred
Seleccioné `Public Route Table` en la sección de `Route Tables` y realicé las siguientes dos configuraciones:
- Agregar ruta al Internet Gateway (IGW): añadí una nueva ruta con destino `0.0.0.0/0` (todo el tráfico de internet), elejí Internet Gateway como destino (`Target`), seleccioné el IGW de mi `Test VPC` y luego guardé los cambios.
- Asociar la subred: En la pestaña `Subnet associations`, seleccioné la subred que creé anteriormente y guardé la asociación para que tenga acceso a internet.

### Paso 6: Crear y configurar la Network ACL (NACL)
En el menú de la izquierda seleccioné `Network ACLs`, luego creé `network ACL` y la configuré con el nombre `Public Subnet NACL`. Una vez creada, la seleccioné de la lista y modifiqué sus reglas de entrada y salida:
- Reglas de entrada (Inbound): En la pestaña `Inbound rules`, añadí una nueva regla con el número `100` y el tipo `All traffic`
- Reglas de salida (Outbound): En la pestaña `Outbound rules`, añadí otra regla con el número `100` y seleccioné `All traffic` para permitir el flujo completo de datos.

### Paso 7: Crear y configurar el Security Group
En el menú de la izquierda seleccioné `Security Groups`, creé el security group y lo configuré para permitir los accesos necesarios hacia la instancia EC2:
- Reglas de entrada (Inbound): Añadí tres reglas para permitir el tráfico de tipo `SSH`, `HTTP` y `HTTPS` desde cualquier origen `(0.0.0.0/0)`.
- Reglas de salida (Outbound): Dejé la configuración por defecto que permite todo el tráfico hacia el exterior. 

### Paso 8: Lanzar la instancia EC2
Lancé la instancia y configuré la máquina con los siguientes detalles:
- Nombre: Lo dejé en blanco.
- Sistema Operativo (AMI): Seleccioné `Amazon Linux 2023 AMI`.
- Tipo de instancia: `t3.micro`.
- Key pair: `vockey`.
- Configuración de red (Network settings): Elegí `Test VPC`, la subred `Public Subnet`, y habilité el `Auto-assign public IP`. En el firewall, marqué `Select existing security group` y elegí el grupo de seguridad que creé antes.

Finalmente lancé la instancia y luego en verifiqué que el estado de mi servidor cambiara de Pending a Running.

### Paso 9: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.

### Paso 10: Probar la conectividad a internet
Una vez dentro del servidor, ejecuté el siguiente comando para verificar que la red esté bien configurada y tenga salida a internet
