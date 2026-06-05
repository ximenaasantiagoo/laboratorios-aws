# <span style="color: #f3b4dd !important;">Lab: Introducción a Amazon EC2</span>

> **Tags:** `Amazon EC2` `Máquina Virtual` `AWS`

---

## Objetivo
El propósito de este laboratorio fue dominar la gestión de instancias en Amazon EC2. Aprendimos a lanzar una máquina virtual, protegerla con Security Groups, monitorear su estado, redimensionar sus recursos de cómputo y almacenamiento, y asegurar su disponibilidad configurando la protección contra terminación para evitar borrados accidentales en la infraestructura.

### 1. Lanzamiento de la Instancia EC2
Para iniciar el servidor virtual, se configuró una instancia en la consola de AWS con las siguientes especificaciones técnicas:

* **Nombre de la Instancia:** `Web Server`
* **Sistema Operativo (AMI):** `Amazon Linux 2023`
* **Tipo de Instancia:** `t3.micro` (2 vCPU, 1 GiB de memoria)
* **Seguridad:** Se procedió sin par de llaves (`Key pair`) debido a que no se requería acceso por SSH.
* **Red:** Despliegue dentro de la `Lab VPC`.
