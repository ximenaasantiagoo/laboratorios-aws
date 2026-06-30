# Lab: Comandos de solución de problemas del protocolo de Internet

> Objetivo: Identificar cómo puedes usar estos comandos en escenarios de clientes

### Paso 1: Conexión a la instancia EC2 mediante SSH
Descargué la llave privada y la IP pública desde AWS. Luego, desde la terminal en la carpeta de descargas, aseguré los permisos de la llave y me conecté al servidor, aceptando la autenticidad del host en el primer acceso.
![imagen1](https://github.com/ximenaasantiagoo/laboratorios-aws/blob/main/images/redes/lab20/paso1.png?raw=true)

### Paso 2: Prueba de conectividad
Para checar si mi instancia EC2 realmente tenía salida a internet, usé el comando `ping` apuntando a la IP `8.8.8.8` (que es el DNS de Google). Con la opción `-c 5` le indiqué que solo mandara 5 mensajes para que no se quedara corriendo infinitamente.

Hacer esto sirvió para confirmar que el internet funcionaba bien y que los permisos de seguridad de AWS (como los Security Groups y las ACL de red) sí estaban dejando pasar este tipo de tráfico.

### Paso 3: Rastrear la ruta del internet 
Para ver todo el camino que recorren mis datos desde la instancia hasta llegar a su destino, usé el comando `traceroute`. Esto sirve cuando la conexión está lenta o se cortan los datos, porque te ayuda a saber si la culpa es de AWS o del proveedor de internet. 

### Paso 4: Revisar puertos 
Para simular una auditoría de seguridad y revisar si había algún puerto sospechoso o comprometido aceptando conexiones en mi servidor, usé el comando `netstat`. Esto me dió las conexiones activas en la capa 4 del modelo OSI (transporte) para saber qué programas están esperando conexiones desde fuera:

- Para ver las conexiones que ya están bien establecidas: `netstat -tp`
- Para ver qué servicios que están esperando conexiones: `netstat -tlp`
- Para ver qué puertos están abiertos para recibir datos, pero mostrando el número directo en lugar de su nombre: `netstat -ntlp` 

### Paso 5: Validar bloqueos de puertos 
Para comprobar si los filtros de seguridad de AWS (como los Security Groups o las ACL de red) realmente estaban bloqueando o permitiendo puertos específicos, utilicé `telnet`. Como no venía instalada por defecto en la instancia, primero la instalé: 

 `sudo yum install telnet -y`

Ya instalada, hice una prueba conectándome a Google por el puerto 80 (el puerto clásico de internet sin cifrar): 

`telnet www.google.com 80`

### Paso 6: Validar servicios web en la capa de aplicación
Para cerrar las pruebas, subí hasta la capa 7 (aplicación) para verificar si un servidor web (como Apache o cualquier página de internet) está funcionando bien y respondiendo con un estado exitoso. Para esto usé el comando `curl`, que sirve para transferir datos y probar la comunicación directa entre mi instancia y un servidor usando protocolos como `HTTP` o `HTTPS`.

`curl -vLo /dev/null https://aws.com`

