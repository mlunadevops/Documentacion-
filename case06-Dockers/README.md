# TECHNICAL LOG & DOCKER FOUNDATIONS

## Traffic Manipulation via the Weight Attribute
**CCNP Miguelangel Luna**

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |
| **02** | [Packet Tracert & VS CODE](./case-02-PT-MCP-VS-Code/) | Conecta Packet Tracert con MCP |
| **03** | [Generar un Archivo Word desde Markdown usando Phyton](./case-03-Markdown-Word-Using-Phyton/) | Convierte un MD a Word usando Phyton |
| **04** | [GNS3 AI](./case04-GNS3-AI/) | Conexion GNS3 MCP. |

[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework

The Weight attribute is a Cisco proprietary parameter used in BGP (Border Gateway Protocol) for best path selection. Its main characteristics are:

* **Local Scope:** It has meaning exclusively within the local router where it is configured and is not propagated via BGP routing updates to neighbors.
* **Value Range:** An integer number between 0 and 65,535.
* **Default Values:** Routes originated locally by the router receive a weight of 32,768 by default; routes learned from external or internal neighbors receive a weight of 0 by default.
* **Precedence:** It is evaluated in the absolute first place within BGP's decision algorithm (above Local Preference, AS_PATH, MED, etc.). Routes with a higher Weight value have absolute preference.

## 2. Implementation

### Paso 1: Creación de la Estructura Base de Directorios

Para mantener un orden de nivel empresarial, lo primero que haremos es crear la carpeta principal del proyecto y sus subdirectorios para persistencia (como SQLite y logs) directamente desde tu terminal de PowerShell o comandos en Windows 10.

**Instrucciones para ti:**
* Abre tu terminal de PowerShell en Windows 10.
* Ejecuta los siguientes comandos uno por uno para crear la estructura limpia del proyecto:

**POWERSHELL**
```text
cd C:\
New-Item -ItemType Directory -Path "C:\Enterprise-MCP-Toolkit" -Force
```

![Creacion Carpetas](images/01Creacioncarpetas.png)

**POWERSHELL**
```text
cd C:\Enterprise-MCP-Toolkit
New-Item -ItemType Directory -Path "data" -Force
New-Item -ItemType Directory -Path "logs" -Force
```
 
![Creacion Carpetas](images/02Creacioncarpetas.png)

### Paso 2: Creación del archivo de dependencias (requirements.txt)

Ahora avanzamos al siguiente nivel. Como necesitamos que nuestro servidor MCP maneje protocolos de red y la estructura del protocolo MCP en Python, vamos a declarar las dependencias técnicas de forma limpia.
* **¿Qué hacemos?:** Creamos un archivo de texto plano llamado `requirements.txt` dentro de la carpeta del proyecto que lista las librerías externas de Python que nuestro software necesita para funcionar (como `mcp`, `netmiko` para red, etc.).

* **¿Para qué sirve?:** Sirve como un manifiesto o lista de compras para Docker y Python. En lugar de instalar las herramientas una por una de forma manual, Docker lee este archivo durante la construcción del contenedor (`docker build`) y descarga automáticamente todas las librerías necesarias de golpe. Esto garantiza que tu kit sea portátil y funcione exactamente igual en cualquier computadora donde lo despliegues.

Instrucciones para ti:
Asegúrate de seguir ubicado en la ruta del proyecto en tu PowerShell **(C:\Enterprise-MCP-Toolkit)** .

Ejecuta el siguiente comando para crear y poblar el archivo **requirements.txt**  con las librerías necesarias:


**POWERSHELL**
```text
@"
mcp
pydantic
netmiko
requests
"@ | Out-File -Encoding utf8 requirements.txt
```

![Creacion Carpetas](images/03Creacionrequirrements.png)



### 1. Crear el archivo `requirements.txt`: Gestión de Dependencias



**Instrucciones para ti:**
* Asegúrate de seguir ubicado en la ruta del proyecto en tu PowerShell (`C:\Enterprise-MCP-Toolkit`).
* Ejecuta el siguiente comando para crear y poblar el archivo `requirements.txt` con las librerías necesarias:

## 3. BGP Configuration:

**Router A (RTA - AS 100):**

```text
! 
router bgp 100
!
```

### 4. BGP Configuration:
