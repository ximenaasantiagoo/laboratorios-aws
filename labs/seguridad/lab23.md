# Lab: Endurecimiento de la red

> Objetivo: Usar Amazon Inspector para buscar fallas de seguridad en una función Lambda de AWS y arreglarlas actualizando el código.

### Paso 1: Activar Amazon Inspector
Entré al servicio de **Amazon Inspector** en la consola de AWS y le di clic al botón **Activate Inspector**. Esperé un par de minutos a que el panel principal marcara 100% en funciones Lambda, lo que significaba que ya había terminado de revisar todo nuestro sistema. 

### Paso 2: Revisar las fallas encontradas
Fui a la sección **All findings** y encontré una falla de nivel medio llamada `CVE-2023-32681 - requests`.

Al darle clic, el panel de ayuda me explicó que la librería de Python llamada `requests` que usaba nuestra aplicación estaba muy vieja y tenía un hueco de seguridad. La recomendación fue cambiarla por una versión más nueva.


### Paso 3: Arreglar el código en Lambda
Para solucionarlo, fui al servicio de **Lambda** y abrí la función `get-request`. Me metí al archivo `requirements.txt` (que es la lista de paquetes que la función necesita para trabajar)

```text
requests==2.20.0

```

Borré el número y los signos de igual para dejar solamente la palabra `requests`. Después, le di al botón **Deploy** para guardar los cambios. Al quitarle el número de versión viejo, obligo a AWS a instalar la versión más nueva y segura de internet cada vez que la función se use.

### Paso 4: Confirmar que todo quedó seguro
Regresé a **Amazon Inspector** para verificar el estado de la red. Cambié el filtro de alertas de Active a Closed y vi que la falla de `requests` ya aparecía como solucionada.