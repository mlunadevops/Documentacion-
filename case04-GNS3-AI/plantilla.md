# TECHNICAL LOG & BGP ENGINEERING GUIDE

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

## 2. Topology and BGP Neighbor Establishment

The topology consists of four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

![BGP WEIGTH](images/01Topologia.jpg)

 four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

## 3. BGP Configuration:

**Router A (RTA - AS 100):**

```text
! 
router bgp 100
!
```

### 4. BGP Configuration:



Lab - Explore the Evolution of Password Methods
Objetivos
Parte 1: Iniciar la VM DEVASC
Parte 2: Explorar código Python que almacena contraseñas en texto plano
Parte 3: Explorar código Python que almacena contraseñas utilizando hash
Antecedentes / Escenario
En este laboratorio, crearás una aplicación que almacena un nombre de usuario y una contraseña en texto plano dentro de una base de datos utilizando código Python. Posteriormente, verificarás que las credenciales se almacenaron correctamente y que un usuario puede utilizarlas para iniciar sesión.

Después realizarás el mismo proceso utilizando una contraseña hasheada para que las credenciales no puedan leerse directamente. Es importante almacenar credenciales y otros datos de manera segura para evitar que distintos servidores y sistemas sean comprometidos.

Recursos requeridos
1 PC con el sistema operativo de tu elección
VirtualBox o VMware
Máquina virtual DEVASC
Instrucciones
Parte 1: Iniciar la VM DEVASC
Si aún no has realizado el laboratorio Install the Virtual Machine Lab Environment, hazlo ahora. Si ya lo completaste, inicia la VM DEVASC.

Parte 2: Demostrar la aplicación
La aplicación primero almacena un nombre de usuario y contraseña en texto plano dentro de una base de datos accesible mediante un servicio web.

Posteriormente valida que las credenciales fueron almacenadas correctamente y funcionan.

El segundo método utiliza hashing para almacenar la contraseña y luego también verifica su funcionamiento.

Parte 3: Instalar paquetes y crear un servicio web
En esta parte utilizarás Flask para crear un servicio web simple que requiere autenticación de usuarios.

La autenticación de usuarios requiere una base de datos, la cual será proporcionada mediante SQLite.

Paso 1: Abrir el directorio security en VS Code e instalar paquetes Python
Abre VS Code.
Selecciona:

File > Open Folder...

Navega al directorio:

devnet-src/security
Haz clic en OK.

En el panel EXPLORER, abre el archivo:

password-evolution.py
Abre una terminal:

Terminal > New Terminal
Instala los paquetes necesarios:

pip3 install pyotp
pip3 install flask

