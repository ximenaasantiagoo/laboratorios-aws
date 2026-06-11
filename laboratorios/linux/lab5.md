# Lab: Edición de Archivos
> ### Objetivo:
> Desarrollar habilidades prácticas en la edición y manipulación de archivos en entornos Linux utilizando los editores de texto `vim` y `nano`.

### Paso 1:Conectarse a la instancia EC2 de Amazon Linux mediante SSH (Mac/Linux)
Para obtener las claves de acceso, descargué el archivo de la llave privada seleccionando el botón Download PEM (se guardó como labsuser.pem). Posteriormente copié y guardé la dirección PublicIP que aparece en ese mismo panel. Cerré el panel de detalles haciendo clic en la `X`. 

### Paso 2: Iniciar la sesión interactiva de Vimtutor
Para comenzar a aprender los comandos básicos del editor `Vim`, ejecuté el tutor interactivo desde la terminal.

### Paso 3: Completar las lecciones prácticas (Lecciones 1-3)
  * Una vez dentro de la interfaz de vimtutor, seguí las instrucciones en pantalla para completar las tareas de las lecciones 1, 2 y 3. Practiqué los comandos esenciales de navegación de cursor (utilizando `h`, `j`, `k`, `l`), así como la inserción, modificación y eliminación básica de texto dentro del entorno del editor. 

  * Tras concluir las primeras tres lecciones y para regresar a la línea de comandos principal de la terminal, cerré el tutor sin guardar los cambios de práctica ejecutando el comando de salida forzada de Vim (`:q!`)
### Paso 5: Crear y editar un archivo nuevo en Vim
 * Inicié el editor `Vim` creando un nuevo archivo de texto con el nombre `helloworld`
 * Una vez dentro del entorno de edición, presioné la tecla `i` para activar el modo de inserción
 * Para salir del modo de inserción, presioné la tecla `ESC`. Finalmente, guardé los cambios realizados y cerré el archivo ejecutando el comando (`:wq`)
   
### Paso 6: Modificar el archivo existente sin guardar cambios
 * Recuperé el último comando y volví a abrir el archivo para realizar una modificación
 * Activé nuevamente el modo de inserción con `i` y añadí la siguiente línea
 * Presioné `ESC` para salir del modo de inserción y para salir del editor sin conservar las modificaciones recientes, utilicé el comando de salida forzada (`:q!`)

### Paso 7: Crear y editar un archivo nuevo en Nano
Para experimentar con un editor de texto alternativo en la terminal, utilicé el comando `nano` seguido del nombre del nuevo archivo. A diferencia de Vim, la interfaz de Nano permite la escritura directa desde el inicio sin necesidad de activar un modo de inserción previo.

### Paso 8: Guardar cambios y salir del editor Nano
Para almacenar de forma permanente el texto introducido y cerrar el entorno del editor, ejecuté las siguientes combinaciones de teclas `CTRL + O` para solicitar la escritura del archivo (WriteOut). Presioné `Enter` para confirmar el nombre predeterminado del archivo (cloudworld). Y por último `CTRL + X` para salir (Exit) de la interfaz de Nano de manera segura.

### Paso 9: Verificar los datos en Nano
En la terminal, volví a abrir el documento para comprobar que los cambios se hubieran guardado de manera correcta. Por último volví a utlizar `CTRL + X` para finalizar y regresar de forma definitiva al prompt de la instancia. 




