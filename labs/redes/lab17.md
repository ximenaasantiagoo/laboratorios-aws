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
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso1.png?raw=true)

### Paso 2: Anotar IPs Iniciales
Esperé a que el estado estuviera en ejecución (2/2 checks). Luego, seleccioné la instancia, y en la pestaña de Networking obtuve la Public IPv4 inicial y la Private IPv4 inicial. 
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso2.png?raw=true)

Posteriormente apagué la instancia y observé que la IP Pública desaparece por completo, mientras que la IP Privada se mantiene guardada.
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso2.1.png?raw=true)

Encendí de nuevo la Instancia y revisé la pestaña Networking para comparar las nuevas IPs. 
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso2.2.png?raw=true)

Observé que la IP Pública cambió a una completamente nueva, pero la IP Privada se quedó exactamente igual. Es decir la IP Pública es Dinámica (cambia con cada reinicio), mientras que la IP Privada es estática dentro de la red local de AWS (no cambia). Por lo tanto, comprobamos el problema de Bob, que al apagar la máquina para ahorrar dinero, la IP pública se destruye y cambia.
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso2.3.png?raw=true)

### Paso 3: Desarrollar la Solución (Asignar la Elastic IP)
Para que Bob tenga una IP fija que no cambie jamás, hice lo siguiente:
- Solicitar la IP Fija (Elastic IP): En el menú izquierdo de EC2, fui a Network & Security luego en Elastic IPs hice clic en Allocate Elastic IP address en la esquina superior derecha y luego en Allocate (dejé todo por defecto). Anoté esa IP.
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso3.png?raw=true)
- Asociar la IP a la Máquina de Bob: Seleccioné la Elastic IP que acababa de crear. Fui al menú superior Actions y luego a Associate Elastic IP address. Mantuve el tipo de recurso como "Instance", busqué en la lista `test instance`, en el campo de "Private IP address", seleccioné la IP privada de mi máquina. Finalmente, hice clic en Associate.
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso3.1.png?raw=true)

### Pasp 4: Pruebas de Validación 
Regresé a la sección de Instances, seleccioné mi máquina y abrí la pestaña de Networking. Observé la dirección Public IPv4 de mi instancia ahora reflejaba exactamente el mismo valor de la Elastic IP que configuré en el paso anterior.
![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso4.png?raw=true)

Finalmente cambié el estado a Stop instance, esperé a que se detuviera por completo y luego la encendí de nuevo con Start instance.
![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso4.1.png?raw=true)
![imagen8](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab17/paso4.2.png?raw=true)

### Conclusiones 
Tras apagar y encender la instancia, la dirección IP Pública no cambió. Se mantuvo fija y persistente con el valor de la Elastic IP. Con esta solución, Bob ya puede apagar su servidor EC2 sin ningun problema, para ahorrar dinero. Cuando vuelva a encenderlo, la IP seguirá siendo la misma, garantizando que sus recursos vinculados no se vuelvan a desconectar ni a romper.
