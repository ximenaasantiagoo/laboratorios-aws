# Lab: Endurecimiento de sistemas

> Objetivo: Mantener actualizados y seguros los sistemas operativos de la empresa creando reglas automáticas de parches (baselines). Aplicar parches por defecto en servidores Linux y crear una regla personalizada para servidores Windows usando grupos de parches.

### Paso 1: Actualizar servidores Linux con la regla por defecto
Para empezar, busqué el servicio **Systems Manager** y fui a **Fleet Manager** para confirmar que el laboratorio ya tenía listos 6 servidores (3 Linux y 3 Windows) vinculados correctamente.

Como AWS ya incluye reglas listas para Linux, decidí parchar los servidores de inmediato:

- Fui a Patch Manager y di clic en Patch now.
- En operación seleccioné Scan and install y en reinicio dejé Reboot if needed.
- Para no alterar otros servidores, elegí buscar por etiquetas (*tags*) e introduje la del grupo de Linux: Clave `Patch Group` y Valor `LinuxProd`.

Le di a Patch now y esperé unos minutos hasta ver que las 3 instancias Linux terminaron de actualizarse con éxito.


### Paso 2: Crear una regla personalizada para Windows

Para los servidores Windows el cliente nos pidió un control más estricto con las actualizaciones de seguridad. Fui a la pestaña **Patch baselines** y creé una regla personalizada llamada `WindowsServerSecurityUpdates`:

- **Sistema Operativo:** Windows.
- **Regla 1 (Crítica):** Seleccioné el producto `WindowsServer2019`, severidad Critical y clasificación SecurityUpdates, con aprobación automática a los 3 días.
- **Regla 2 (Importante):** Añadí otra regla idéntica pero para severidad Important.

Una vez guardada, seleccioné mi nueva regla, fui a Actions luego en Modify patch groups y escribí el nombre de grupo `WindowsProd`. Esto vincula la regla con los servidores que tengan esa etiqueta.


### Paso 3: Etiquetar y actualizar los servidores Windows
Antes de lanzar la actualización de Windows, tuve que ir al servicio de EC2 para ponerle la etiqueta correspondiente a las 3 instancias de Windows (`Windows-1`, `Windows-2` y `Windows-3`), ya que estas no venían listas de fábrica.



Con las etiquetas listas, regresé a Patch Manager, le di a Patch now y repetí la configuración de escaneo e instalación, pero esta vez filtrando por la etiqueta `WindowsProd`. Al arrancar, entré al código de ejecución (`Execution ID`) para ver en el *Output* cómo el sistema aplicaba los parches de seguridad en segundo plano.


### Paso 4: Verificar el cumplimiento de seguridad (Compliance)
Para cerrar el laboratorio, fui a comprobar que todos los equipos estuvieran al día y seguros. En el menú de Patch Manager, entré a la pestaña Dashboard.

En el resumen de cumplimiento (*Compliance summary*) pude confirmar `Compliant: 6`, lo que significa que los 3 servidores Linux y los 3 de Windows quedaron parchados.
