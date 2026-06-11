# Lab: Trabajo con el sistema de archivos

> ### Objetivo:
> Dominar la administración de archivos y carpetas en Linux mediante el uso de la terminal. Crear, copiar, mover y eliminar elementos para gestionar el sistema de forma eficiente.

### Paso 1:Conectarse a la instancia EC2 de Amazon Linux mediante SSH (Mac/Linux)
Para obtener las claves de acceso, descargué el archivo de la llave privada seleccionando el botón Download PEM (se guardó como labsuser.pem). Posteriormente copié y guardé la dirección PublicIP que aparece en ese mismo panel. Cerré el panel de detalles haciendo clic en la `X`. 

### Paso 2: Estructura a crear
El objetivo inicial es replicar el siguiente árbol de directorios y archivos en la máquina virtual

```text
/home/ec2-user/CompanyA/
├── Finance/
│   ├── ProfitAndLossStatements.csv
│   └── Salary.csv
├── HR/
│   ├── Assessments.csv
│   └── TrialPeriod.csv
└── Management/
    ├── Managers.csv
    └── Schedule.csv
```
  * Primero, verifiqué mi ubicación actual con `pwd`. Si no me encontraba en la ruta correcta, utilicé `cd /home/ec2-user`.
  * Creé la carpeta principal `mkdir CompanyA`
  * Cambié mi directorio a la carpeta recientemente creada `cd CompanyA`
  * Posteriormente, creé las tres subcarpetas en un solo comando `mkdir Finance HR Management`
  * Verifiqué que las carpetas se crearon correctamente con Cambié el directorio a la carpeta Finance para poder crear los archivos correspondientes

### Paso 3: Crear archivos en la carpeta Finance
  * Cambié el directorio (`cd`) a la carpeta Finance para poder crear los archivos correspondientes
  * Creé los archivos vacíos utilizando el comando `touch`
  * Verifiqué que los archivos se crearon correctamente con el comando `ls`

### Paso 4: Crear archivos en la carpeta Management
  * Regresé a la carpeta raíz y creé los archivos directamente especificando su ruta `touch Management/Managers.csv Management/Schedule.csv`
  * Verifiqué que los archivos se crearon de manera correcta con el comando `ls Management`

### Paso 5: Crear archivos en la carpeta HR
Repetí un proceso similar para generar los archivos de la carpeta HR utilizando el comando `touch HR/Assessments.csv HR/TrialPeriod.csv`

### Paso 6: Validación Final de la Estructura
Para verificar que todos los archivos y carpetas de `CompanyA` se crearon correctamente, con sus respectivos permisos y rutas, ejecuté el comando de listado recursivo `ls -laR`

### Paso 7: Reestructuración (Copiar carpetas y manejo de errores al eliminar)
  * Primero, copié la carpeta Finance junto con todo su contenido dentro de la carpeta HR de manera recursiva `cp -r Finance HR`
  * Verifiqué la copia, listando el interior del destino con `ls HR/Finance`
  * Posteriormente, intenté borrar la carpeta Finance original del directorio `raíz con rmdir Finance`, pero el sistema arrojó un error debido a que la carpeta no estaba vacía. Para solucionarlo sin usar comandos destructivos directos, eliminé primero los archivos internos de forma manual `rm Finance/ProfitAndLossStatements.csv Finance/Salary.csv`
  * Una vez vacía la carpeta, ejecuté rmdir Finance para dorelos eliminar del directorio raíz
    
### Paso 8: Reestructuración (Mover y organizar subcarpetas)
  * Trasladé el directorio de Management para que quedara alojado de forma interna en HR usando el comando`mv` (move)
  * Verifiqué el cambio revisando tanto la raíz como la nueva subruta con  `ls . HR/Management`
  * Cambié el directorio a Recursos Humanos con `cd HR` y creé una nueva carpeta para organizar al personal `mkdir Employees`
  * Luego, moví los archivos de evaluaciones y periodos de prueba dentro de esta nueva carpeta `mv Assessments.csv TrialPeriod.csv Employees`
  * Finalmente verifiqué la organización final ejecutando `ls . Employees`

