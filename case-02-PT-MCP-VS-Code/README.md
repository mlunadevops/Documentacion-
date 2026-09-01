# Integración de MCP con Cisco Packet Tracer y VS Code:

Este documento detalla el paso a paso para configurar la integración de Protocolo de Contexto de Modelo (MCP) entre Cisco Packet Tracer y Visual Studio Code, incluyendo la configuración del entorno de desarrollo local, archivos de seguridad y despliegue de módulos.

## Fase 1: Configuración del Backend y Seguridad

### 1. Clonación del Repositorio Local

Abre una terminal de PowerShell y clona el repositorio oficial del proyecto en tu máquina local:

```text
cd ~
git clone https://github.com/Mats2208/MCP-Packet-Tracer.git
```
![MCP Packet Tracer](images/2Clone.png)

### 2. Creación del Entorno Virtual e Instalación de Dependencias:

Entra a la carpeta del proyecto, crea y activa tu entorno virtual de Python, actualiza `pip` e instala el paquete en modo editable:

```text
cd MCP-Packet-Tracer
python -m venv venv
.\venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -e .
```

![MCP Entorno Virtual](images/2Entornovirtual.png)
