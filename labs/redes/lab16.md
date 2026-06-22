# Lab: Direcciones IP públicas y privadas

> ### Objetivo
> Entender la diferencia entre una dirección IP privada y una pública. 


### Paso 1: Acceso a la Consola de AWS
En la consola de AWS, en la barra de búsqueda superior, escribí EC2 y seleccioné el servicio para abrir el panel de control.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso1.png?raw=true)

### Paso 2: Localización de las Instancias
En el menú lateral izquierdo, fui a la opción `Instances` para ver la lista de los servidores. Identifiqué las dos instancias del laboratorio: `Instance A` e `Instance B`.
![imagen2](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso2.png?raw=true)

### Paso 3: Registro de Datos de Instance A
Seleccioné la casilla de Instance A. En la sección inferior, abrí la pestaña Networking (Redes). Copié y guardé en mi editor de texto los siguientes datos:
- Nombre de la instancia.
- Dirección IPv4 Pública.
- Dirección IPv4 Privada.
![imagen3](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso3.png?raw=true)

### Paso 4: Registro de Datos de Instance B
Desmarqué la instancia anterior y seleccioné la casilla de `Instance B`. Revisé la pestaña Networking en la parte inferior Copié y guardé en mi editor de texto los datos correspondientes de la Instancia B, similar al paso anterior.
![imagen4](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso4.png?raw=true)

### Paso 5: Comparación de Direcciones
Revisé y comparé los datos que guardé de ambas instancias en mi editor de texto. Analicé las diferencias entre sus direcciones IP (públicas y privadas) para empezar a buscar la razón por la cual una tiene internet y la otra no.


### Paso 6: Descarga de Credenciales y Conexión SSH (Mac/Linux)
Abrí el menú desplegable `Details` arriba de las instrucciones y seleccioné `Show` para ver las credenciales.
Descargé el archivo de la llave (`labsuser.pem`) y cerré el panel.
![imagen5](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso6.png?raw=true)


Abrí una terminal en mi computadora y me cambié al directorio donde se descargó el archivo. Cambié los permisos de la llave para que fuera de solo lectura. 
![imagen6](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso6.1.png?raw=true)


Finalmente intenté conectarme a la Instance A mediante SSH con el siguiente comando (usando su dirección IP correspondiente)
![imagen7](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab16/paso6.2.png?raw=true)

### Conclusiones 
Para conectarme desde mi computadora fuera de AWS, es obligatorio utilizar una dirección IP pública, ya que las IP privadas no son accesibles a través de internet. Por esta razón, solo ppdía conectarme mediante SSH a Instance B, la cual cuenta con una dirección IP pública asignada que permite el acceso desde el exterior. En cambio, la conexión a Instance A no fue posible y provocó un bloqueo (timeout) en mi terminal, debido a que solo tiene asignada una dirección IP privada que no tiene enrutamiento hacia internet, impidiendo cualquier comunicación directa desde fuera de la VPC.

