# Lab: Direcciones IP estáticas y dinámicas

> ### Objetivo
> Analizar el impacto del direccionamiento IP dinámico frente al estático en instancias EC2 para mitigar pérdidas de conectividad. Posteriormente, se implementará una solución persistente mediante la asignación de una IP elástica (Elastic IP) que resuelva la problemática del cliente.

### Paso 1: Replicar el Problema del Cliente (Lanzar la instancia EC2)
Crear la Instancia en la consola de AWS, busqué `EC2` y luego seleccioné `Launch instances`. La instancia tuvo las siguientes características: 
- AMI: Amazon Linux 2 AMI.
- Tipo: t3.micro.
- Configuración: red Lab VPC, la subnet Public Subnet 1 y me aseguré de poner Auto-assign Public IP en Enable (Habilitado).
- Tags: Añadí un Tag con Key (test instance).
- Seguridad y Llave: Security Group llamado Linux Instance SG y usa la llave existente vockey. 

Posteriormente lancé la instancie 

### Paso 2: Anotar IPs Iniciales
Esperé a que el estado estuviera en ejecución (2/2 checks). Luego, seleccioné la instancia, y en la pestaña de Networking obtuve la Public IPv4 inicial y la Private IPv4 inicial


Posteriormente apagué la instancia y observé que la IP Pública desaparece por completo, mientras que la IP Privada se mantiene guardada.


Encendí de nuevo la Instancia y revisé la pestaña Networking para comparar las nuevas IPs. 


Observpe que la IP Pública cambió a una completamente nueva, pero la IP Privada se quedó exactamente igual. Es decir la IP Pública es Dinámica (cambia con cada reinicio), mientras que la IP Privada es estática dentro de la red local de AWS (no cambia). Por lo tanto, comprobamos el problema de Bob, que al apagar la máquina para ahorrar dinero, la IP pública se destruye y cambia.


### Paso 2: Desarrollar la Solución (Asignar la Elastic IP)
Para que Bob tenga una IP fija que no cambie jamás, hice lo siguiente:
- Solicitar la IP Fija (Elastic IP): En el menú izquierdo de EC2, fui a Network & Security luego en Elastic IPs hice clic en Allocate Elastic IP address en la esquina superior derecha y luego en Allocate (dejé todo por defecto). Anoté esa IP.

- Asociar la IP a la Máquina de Bob: Seleccioné la Elastic IP que acababa de crear. Fui al menú superior Actions y luego a Associate Elastic IP address. Mantuve el tipo de recurso como "Instance", busqué en la lista mi test instance y, en el campo de "Private IP address", seleccioné la IP privada de mi máquina. Finalmente, hice clic en Associate.


### Pasp 3: Pruebas de Validación 
Regresé a la sección de Instances, seleccioné mi máquina y abrí la pestaña de Networking. Observé la dirección Public IPv4 de mi instancia ahora reflejaba exactamente el mismo valor de la Elastic IP que configuré en el paso anterior.


Finalmente cambié el estado a Stop instance, esperé a que se detuviera por completo y luego la encendí de nuevo con Start instance.


### Conclusiones 
Tras apagar y encender la instancia, la dirección IP Pública no cambió. Se mantuvo fija y persistente con el valor de la Elastic IP. Con esta solución, Bob ya puede apagar su servidor EC2 sin ningun problema, para ahorrar dinero. Cuando vuelva a encenderlo, la IP seguirá siendo la misma, garantizando que sus recursos vinculados no se vuelvan a desconectar ni a romper.
