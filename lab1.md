# <span style="color: #f3b4dd !important;">Lab: Introducción a Amazon EC2</span>

> **Tags:** `Amazon EC2` `Virtual Machines` `Compute` `AWS`

---

## Objetivo
El objetivo de este laboratorio fue comprender el ciclo de vida de una instancia de cómputo en la nube mediante el lanzamiento, redimensionamiento, monitoreo y gestión de una máquina virtual en Amazon EC2, además de aplicar reglas de firewall con grupos de seguridad y probar la protección contra terminación.

### 1. Lanzamiento de la Instancia EC2
Para iniciar el servidor virtual, se configuró una instancia en la consola de AWS con las siguientes especificaciones técnicas:

* **Nombre de la Instancia:** `Web Server`
* **Sistema Operativo (AMI):** `Amazon Linux 2023`
* **Tipo de Instancia:** `t3.micro` (2 vCPU, 1 GiB de memoria)
* **Seguridad:** Se procedió sin par de llaves (`Key pair`) debido a que no se requería acceso por SSH.
* **Red:** Despliegue dentro de la `Lab VPC`.
