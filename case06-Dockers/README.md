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

jajaja

![Creacion Carpetas](images/00InfografiaBlueprint.jpg)



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

### Paso 2: Creación del archivo de dependencias (requirements.txt) este archivo es tambien llamado (MANIFIESTO de dependencias)

Como necesitamos que nuestro servidor MCP maneje protocolos de red y la estructura del protocolo MCP en Python, vamos a declarar las dependencias técnicas de forma limpia. El archivo **requirements.txt** es la lista de ingredientes (las librerías de Python) a este archivo se le llama **manifiesto**, y el Dockerfile que haremos a continuación será la receta de cocina completa que le dice a Docker cómo juntar esos ingredientes, el sistema operativo base y tu código para hornear el contenedor final.

**Manifiesto de dependencias:** En el ecosistema de Docker y desarrollo moderno, un "manifiesto" es cualquier archivo de configuración declarativo que describe de forma estática lo que un sistema o contenedor necesita para existir y funcionar (como el `requirements.txt` para Python, el `package.json` en Node.js, o el propio `Dockerfile`). Es la "declaración de intenciones" de la aplicación.

* **¿Para qué sirve?:** Sirve como un manifiesto o lista de compras para Docker y Python. En lugar de instalar las herramientas una por una de forma manual, Docker lee este archivo durante la construcción del contenedor **(`docker build`)** y descarga automáticamente todas las librerías necesarias de golpe. **Esto garantiza que tu kit sea portátil y funcione exactamente igual en cualquier computadora donde lo despliegues.**

###**¿Qué pasa si una dependencia ya no existe o cambia de versión?: Gestión de Riesgos y Dependencias**

* **¿Qué analizamos?:** El riesgo de obsolescencia de paquetes o cambios drásticos en los repositorios públicos (como PyPI).
* **¿Qué sucede técnicamente?:** Si una versión exacta declarada desaparece o el repositorio oficial la elimina, el comando de instalación (`pip install`) dentro de Docker fallará al momento de construir la imagen, deteniendo el proceso de despliegue.
* **¿Cómo lo mitigamos a nivel empresarial?:**
  * **Uso de versiones fijas (Pinning):** En entornos de producción críticos, en lugar de poner solo `netmiko`, se especifican versiones exactas (ej. `netmiko==4.3.0`) para garantizar consistencia.
  * **Caché local o espejos privados:** Al empaquetar todo dentro de Docker y mantenerlo en tu kit portátil, una vez que la imagen se construye exitosamente por primera vez, **la imagen compilada ya lleva las librerías dentro. No necesita volver a descargarlas de internet cada vez que la ejecutes, lo que te independiza de futuras caídas de internet o cambios en la web.**

### 2.1 Crear el archivo `requirements.txt`: Gestión de Dependencias

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



## 3. BGP Configuration:

**Router A (RTA - AS 100):**

```text
! 
router bgp 100
!
```

### 4. BGP Configuration:
