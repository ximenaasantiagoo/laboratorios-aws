# Glosario 
> **Amazon EC2 (Elastic Compute Cloud)**
> 
> Servicio web que proporciona servidores virtuales (instancias) con capacidad de cómputo segura y de tamaño modificable en la nube.

> **AMI (Amazon Machine Image):**
>
>  Plantilla preconfigurada que contiene el sistema operativo, el servidor de aplicaciones y el software inicial para lanzar una instancia.

> **Tipo de Instancia (Instance Type):**
>
>  Combinación específica de CPU, memoria, almacenamiento y capacidad de red que determina el hardware y el rendimiento del servidor. Ejemplo `t3.micro`

> **Amazon EBS (Elastic Block Store):** Volúmenes de almacenamiento de bloques de alto rendimiento diseñados para utilizarse con instancias de EC2 (actúan como los "discos duros" virtuales).

> **Volumen Raíz (Root Volume):** El volumen principal de EBS donde se instala el sistema operativo y se utiliza para arrancar (bootear) la instancia.

> **VPC (Virtual Private Cloud):** Red virtual lógicamente aislada dentro de la nube de AWS donde defines tu propia infraestructura de red.

> **Security Group (Grupo de Seguridad):** Firewall virtual a nivel de instancia que controla el tráfico entrante (Inbound) y saliente (Outbound). Por defecto, bloquea todo el tráfico entrante.

> **DNS Público:** Sistema que traduce la dirección IP numérica del servidor en un nombre de dominio legible (texto) para acceder a él desde Internet.

> **User Data (Datos de usuario):** Script o conjunto de comandos que se le pasa a la instancia para automatizar tareas de configuración e instalación de software al arrancar por primera vez.

> **Termination Protection (Protección contra terminación):** Atributo de seguridad que, al estar activo, impide que la instancia sea eliminada o borrada por accidente.

> **Terminar (Terminate):** Acción de eliminar de forma definitiva la instancia EC2 y, por defecto, borrar su volumen raíz asociado. No se puede revertir.
