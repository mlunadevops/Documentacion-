# GNS3 & MCP

## Conexion de GNS3 a traves de un API
**CCNP/CCAI Miguelangel Luna**

r
subrayado
---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |
| **02** | [Packet Tracert & VS CODE](./case-02-PT-MCP-VS-Code/) | Conecta Packet Tracert con MCP |

[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework

Para conectar GNS3 (versión 2.2.60) a un cliente o agente compatible con el protocolo MCP (Model Context Protocol) —en este caso utilizando Gemini AI (por ejemplo, a través de Gemini CLI, extensiones compatibles o entornos de desarrollo)—, la estrategia recomendada consiste en utilizar un servidor MCP especializado para GNS3 que actúe como puente (middleware). Existen servidores comunitarios diseñados específicamente para esto (como `gns3-mcp` o `gns3-mcp-server`) que exponen toda *la API REST de GNS3* y el control de consolas en formato de herramientas MCP.

 **¿Que es un JSON (JSON (JavaScript Object Notation)?**

Es el formato estándar que se utiliza para empaquetar y transportar los datos entre el cliente y el servidor.

 **¿Que es un API REST?**

 El API REST es el sistema completo (el conjunto de reglas y la interfaz) que permite la comunicación, es una arquitectura cliente-servidor basada en HTTP, donde una parte (el cliente) pide un recurso y la otra (el servidor) lo procesa y responde. El REST Es una forma de aplicar ese modelo cliente-servidor utilizando los protocolos que ya existen en la web (principalmente HTTP).

* El canal de transporte físico o la "autopista" por donde viaja todo es **HTTP** (con sus métodos como `GET` y `POST`).
* El idioma o formato en el que va empaquetada la información que viaja por ese canal es **JSON**.

Por lo tanto, el API REST utiliza el protocolo **HTTP** como canal de comunicacion, **JSON** como lenguaje/formato para conectar al cliente con el servidor y el metodo (también conocido como verbo HTTP) son las instrucciones y respuestas que se intercambian, es decir, un método  es la acción explícita que le indica al servidor qué es lo que el cliente quiere hacer con el recurso, por ejemplo: 

Imagina que el recurso es un archivo en una oficina:

* El método `GET` dice: "Quiero ver este archivo".
* El método `POST` dice: "Quiero crear un archivo nuevo".
* El método `PUT` dice: "Quiero reemplazar este archivo por completo".
* El método `DELETE` dice: "Quiero eliminar este archivo".


 
![GNS3 MCP Install](images/00APIrest.jpg)

Esta imagen es un diagrama que ilustra el funcionamiento de una API REST.
Muestra el flujo completo:

* Un Cliente (como una app o navegador) realiza una Solicitud (Request) al Servidor a través de Internet usando métodos HTTP (`GET`, `POST`, etc.).
* El Servidor procesa la petición interactuando con su base de datos.
* El Servidor devuelve una Respuesta (Response) al Cliente, típicamente en formato JSON, confirmando el éxito (`200 OK`) con los datos solicitados.

![GNS3 MCP Install](images/01APIrest.jpg)

## 2. Topologia e Infografia

The topology consists of four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

## 3. Implementacion:

**POWERSHELL**

3.0) Script, el siguiente script se utiliza unicamente para obtener el path de donde esta instalado el Python y crearlo automaticamente esto se hace basicamente, para que desde cualquier lugar que estemos en el prompt de POWERSELL, pueda ser ejecutados los comandos de python.

```text
# 1. Obtener la ruta de los scripts de usuario desde Python y registrarla en el PATH de usuario
$PythonScriptsPath = [System.IO.Path]::Combine([Environment]::GetFolderPath('ApplicationData'), "Python", "Python312", "Scripts")

# Validar y agregar si no existe en el PATH actual del usuario
$UserPath = [Environment]::GetEnvironmentVariable("PATH", "User")
if ($UserPath -notlike "*$PythonScriptsPath*") {
    [Environment]::SetEnvironmentVariable("PATH", "$UserPath;$PythonScriptsPath", "User")
    Write-Host "¡Ruta agregada con éxito al PATH de usuario: $PythonScriptsPath" -ForegroundColor Green
} else {
    Write-Host "La ruta ya se encontraba registrada en el PATH." -ForegroundColor Yellow
}

# 2. Refrescar el PATH para la sesión actual de PowerShell
$env:PATH = [Environment]::GetEnvironmentVariable("PATH", "Machine") + ";" + [Environment]::GetEnvironmentVariable("PATH", "User")
```

3.1) Instalar el Servidor MCP de GNS3: mediante la instalacion del siguiente paquete

**POWERSHELL**

```text
pip install gns3-mcp
```

![GNS3 MCP Install](images/10pipinstallgns3mcp.png)

Opcional para actualizar el servidor MCP de GNS3 realizar lo siguiente:

**POWERSHELL**

```text
python.exe -m pip install --upgrade pip
```

![GNS3 MCP Install](images/12pipinstallgns3mcp.png)


3.2) Verificar la instalacion del Servidor MCP de GNS3.

**POWERSHELL**

```text
pip list | Select-String "gns3-mcp"
```

![GNS3 MCP Install](images/11pipinstallgns3mcp.png)

### Conexión del servidor MCP de GNS3 "gns3-mcp"  (instalado en el paso 3.1 a traves del comando pip install "gns3-mcp") con GNS3 VIRTUAL MACHINE SERVER

3.3)  Conectar el servidor MCP  de GNS3 "gns3-mcp" , para esto hay que tener los datos de conexion de la VM de GNS3, son los siguientes:

```text
IP SERVIDOR VM GNS3 = "10.0.30.50"
PUERTO SERVIDOR VM GNS3 = "80"
USUARIO SERVIDOR VM GNS3 = "gns3"
PASSWORD SERVIDOR VM GNS3 = "gns3"
```

Para que el servidor MCP pueda comunicarse con el GNS3 2.2.60 VIRTUAL MACHINE, necesitamos configurar las variables de entorno que el servidor requiere para la conexion a traves del siguiente script en POWERSHELL:

**POWERSHELL**

```text
# Limpiar variables
Remove-Item Env:\GNS3_* -ErrorAction SilentlyContinue

# Apuntar al puerto de API REST 3080 con la IP de la VM
$env:GNS3_HOST="10.0.30.50"
$env:GNS3_PORT="80"
$env:GNS3_USER="gns3"
$env:GNS3_PASSWORD="gns3"

# Ejecutar el servidor MCP
gns3-mcp
```

En la siguiente imagen podemos verificar que la conexion se realizo correctamente, sin embargo aparece el siguiente error:

En los logs se observa un nuevo error: **`HTTP 404 Not Found`** al intentar autenticarse en la ruta **`http://10.0.30.50/v3/access/users/authenticate`.**

*   **El motivo:** El error `404` significa que la ruta o endpoint de la API no existe en esa dirección. Esto suele ocurrir porque la versión de GNS3 que estás utilizando (la `2.2.60`) utiliza una estructura de rutas distinta en conclusion LA VERSION 2.2.60 DEL GNS3 USA AUTENTICACION V3 mientras que el MCP server utiliza la version V3), **ESTA INCOMPATIBILIDAD DE VERSIONES IMPOSIBILITA LA AUTENTICACION.**
*   **La solución:** Instalar una version de MCP que trabaje con V2 o actualizar la version del GNS3`. 

![GNS3 MCP Install](images/14pipinstallgns3mcp.png)

### SOLUCION TRABAJAR CON OTRA VERSION DE MCP QUE USE AUTHENTICATION V2 LA CUAL ES COMPATIBLE con GNS3 2.2.60 VIRTUAL MACHINE SERVER. EN ESTE CASO LO VOY A DESARROLLAR PERSONALMENTE

### Paso 1: Entrar a la consola interactiva de Python para probar un SCRIPT PERSONALIZADO.

Escribe `python` en tu PowerShell y presiona Enter (esto abrirá el intérprete de Python, donde los comandos `import` y `print` funcionarán perfectamente):

**POWERSHELL**

```text
python
```

```text
import requests
url = "http://10.0.30.50/v2/projects"
response = requests.get(url, auth=("gns3", "gns3"))
print(response.status_code)
print(response.json())
```

![GNS3 MCP Install](images/15python.png)


Ok esta si funciona correctamente


### Paso 1: Instalar las librerías necesarias en Python

Abre tu terminal (PowerShell) en Windows y asegúrate de instalar la librería oficial de MCP de Python y la librería `requests`:

```powershell
pip install mcp requests
```

![GNS3 MCP Install](images/16MCPpersonalizado.png)

### Paso 2: Crear el archivo de tu Servidor MCP Personalizado

Crea una carpeta nueva para tu proyecto (por ejemplo, `gns3-mcp-v2`) y dentro crea un archivo llamado `server.py`. 

Copia y pega este código base en `server.py`. Este script ya incluye la lógica para conectarse a tu GNS3 2.2.60 en el puerto `3080` mediante la API v2:

```powershell
from mcp.server.fastmcp import FastMCP
import requests

# Inicializar FastMCP para tu puente GNS3 v2
mcp = FastMCP("GNS3 v2 Bridge")

GNS3_URL = "http://10.0.30.50/v2"
AUTH = ("gns3", "gns3")

@mcp.tool()
def listar_proyectos() -> str:
    """Lista todos los laboratorios/proyectos disponibles en GNS3 v2."""
    try:
        response = requests.get(f"{GNS3_URL}/projects", auth=AUTH)
        if response.status_code == 200:
            projects = response.json()
            resultado = "Laboratorios encontrados en GNS3:\n"
            for p in projects:
                resultado += f"- Nombre: {p['name']} | Estado: {p['status']} | ID: {p['project_id']}\n"
            return resultado
        return f"Error al obtener proyectos: {response.status_code}"
    except Exception as e:
        return f"Excepción de conexión: {str(e)}"

@mcp.tool()
def controlar_proyecto(project_id: str, accion: str) -> str:
    """Inicia (start) o detiene (stop) un proyecto de GNS3 usando su ID."""
    try:
        # accion puede ser start o stop
        response = requests.post(f"{GNS3_URL}/projects/{project_id}/control/{accion}", auth=AUTH)
        if response.status_code in [200, 204]:
            return f"Acción '{accion}' ejecutada exitosamente en el proyecto {project_id}."
        return f"No se pudo ejecutar la acción. Código: {response.status_code}, Resuesta: {response.text}"
    except Exception as e:
        return f"Excepción al controlar proyecto: {str(e)}"

if __name__ == "__main__":
    mcp.run()
```
### Paso 3: Configurar el Servidor MCP en Visual Studio Code

Para que tu cliente de IA en VS Code (o la aplicación compatible con MCP que utilices) reconozca este servidor, debes declararlo en su archivo de configuración (generalmente llamado `mcp_config.json` o en la configuración de extensiones de MCP).

La ruta de ejecución que le darás a tu cliente de IA apuntará directamente a tu entorno de Python ejecutando tu script:

















------------------------------------------------------------


-----------------------------------------------------------



----------------------------------------------------------











Debes registrar el servidor MCP en el archivo de configuración de tu cliente compatible con Gemini (por ejemplo, en el archivo de ajustes del entorno o settings.json / mcp_config.json):  

```text
{
  "mcpServers": {
    "gns3": {
      "command": "gns3-mcp",
      "env": {
        "GNS3_BASE_URL": "http://10.0.30.50",
        "GNS3_USERNAME": "gns3",
        "GNS3_PASSWORD": "gns3"
      }
    }
  }
}
```

(Nota: Si usas una ruta absoluta o un entorno virtual, asegúrate de apuntar directamente al ejecutable del script o usar uvx gns3-mcp si prefieres gestión de paquetes moderna).

La configuracion del cliente GEMINI para probar la conexion:

### Configuración de Credenciales de GNS3


3.2) Probar la ejecución manual del servidor (Modo Stdio):

**POWERSHELL**

```text
gns3-mcp
```

![GNS3 MCP Install](images/12pipinstallgns3mcp.png)

Dado que el servidor se comunica típicamente por flujos estándar (`stdio`) con el cliente de IA, puedes invocarlo directamente en una terminal para ver si arranca sin arrojar errores de dependencias:

3.3). Validación de la Conexión

Una vez configurado e iniciado tu cliente de Gemini, puedes verificar que las herramientas de GNS3 estén disponibles ejecutando el comando de inspección en tu agente (por ejemplo, /mcp list o solicitándole directamente a Gemini):


### 4. BGP Configuration:
