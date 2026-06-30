# Lab: Solución de problemas de red 

> Objetivo: Ayudar a un cliente que no puede acceder a su servidor web Apache desde su VPC, usando una réplica exacta de su entorno para diagnosticar el problema.

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab21/paso1.png?raw=true)

### Paso 2: Revisar el estado del servidor web Apache
Para empezar a investigar por qué no cargaba la página web de Ana, me conecté al servidor y lo primero que hice fue checar si el servicio de Apache (que en Linux se llama `httpd`) estaba corriendo. Como no soy el usuario raiz, usé `sudo` para tener permisos de administrador.   


Al revisar la terminal, vi que el servicio aparecía como inactive. Esto significa que el programa sí está instalado en el servidor, pero está completamente apagado.

### Paso 3: Encender el servicio y probar en el navegador
Como el servicio estaba apagado, procedí a encenderlo con el comando `start` y volví a verificar su estado para asegurarme de que ya estuviera activo.

`sudo systemctl start httpd.service`
`sudo systemctl status httpd.service`

Ahora que la terminal me mostraba el servicio en verde como active (running), copié la IP pública de mi instancia y la pegué en una pestaña nueva del navegador.

`http://<TU_IP_PÚBLICA>`

A pesar de que el servidor ya estaba encendido por dentro, la página web se quedó cargando y no abrió. Esto me confirmó que el problema no era el programa Apache, sino algo en la red de AWS.

### Paso 4: Investigar la configuración de la VPC en AWS
Al ver que el navegador no conectaba, entré a la consola de AWS para revisar la arquitectura de la red (la VPC) y encontrar qué estaba bloqueando el camino. Fui al servicio de VPC y empecé a revisar lo siguiente:
- Subnets: ¿Están asociadas a la tabla de ruteo correcta?
- Route Tables: ¿Tienen una ruta configurada que apunte hacia internet?
- Internet Gateway (IGW): ¿Existe un puente a internet y está conectado a nuestra VPC?
- Security Groups y Network ACLs: ¿Están los permisos configurados para dejar pasar el tráfico?


### Paso 5: Confirmación del servicio funcionando. 
Una vez que corregí el problema detectado en la configuración de red en AWS, volví a ingresar a mi navegador web e introduje de nuevo la dirección
