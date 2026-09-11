# TECHNICAL LOG & IMPLEMENTACION IA LOCAL

## Implementacion de Modelo Fundacional de forma local
**CCNP Miguelangel Luna** P.ssw.rd2018

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |
| **02** | [Packet Tracert & VS CODE](./case-02-PT-MCP-VS-Code/) | Conecta Packet Tracert con MCP |

[Google](https://www.google.com)

****

## 1. Introduction and Theoretical Framework

**Inferencia:** Se refiere al momento en que el modelo procesa una pregunta (prompt) y genera una respuesta.

**Motor de inferencia (inference engine):**  Software encargado de cargar un modelo de IA en la (RAM o VRAM) y ejecutar los cálculos matemáticos necesarios para procesar un texto de entrada (*prompt*) y generar una respuesta (inferencia). En este proyecto vamos a usar **OLLAMA**. **Ollama** es el reproductor de video y los modelos fundacionales **(Phi-3.5 o Qwen 2.5)** son las películas.

**Modelo Fundacional:** Es una IA a gran escala entrenada con volúmenes masivos de datos. Sirve como una base flexible y multipropósito que se puede adaptar fácilmente mediante instrucciones o ajustes para realizar miles de tareas diferentes (como escribir, programar o analizar datos), en lugar de estar limitada a una sola función específica.  En este proyecto vamos a usar los modelos fundacionales **(Phi-3.5 o Qwen 2.5)**.

**Modelo Fundacional Pequeño (*Small Language Model*):** es un modelo de IA entrenado a gran escala —igual que los modelos gigantes—, pero diseñado con una cantidad reducida de parámetros (por lo general, menos de 10 mil millones). Ejemplos de SML:

* **Phi-3.5 Mini (3.8B):** Excelente velocidad y bajo consumo de RAM.
* **Qwen 2.5 (7B):** Muy superior en tareas de análisis sintáctico de código.

**Nota:** **Los modelos SML como Phi-3.5 Mini o Qwen 2.5 son los cerebros (los archivos de pesos neuronales que Ollama ejecuta)**. Son los archivos pesados (de varios gigabytes) que ya vienen entrenados con millones de datos y que contienen todo el conocimiento para redactar, programar o analizar código.

**El Backend (El motor y el cerebro):** El Backend de esta arquitectura esta conformada por **Ollama (motor/reproductor)**  y el FM (Conocimiento) **(Phi-3.5 o Qwen 2.5)**  Ambos viven y solo pueden operar juntos (son dependientes) en tu VM de Ubuntu Server.

* **Ollama:** Funciona como el servidor de aplicaciones y motor de ejecución o reproduccion del FM.
* **El modelo fundacional (ej. Phi-3.5 o Qwen 2.5):** Es el conjunto de datos y pesos neuronales que procesa la información (conocimiento).

**Cliente LLM (*frontend*):**  Aplicación con la que el usuario humano) o tus programas interactúan directamente. El cliente le envía la pregunta a Ollama, este la procesa con el FM **(Phi-3.5 o Qwen 2.5)**, mostrandote la respuesta formateada. En este proyecto vamos a utilizar **Open WebUI**.

**¿Que es (Open WebUI) (*frontend*)?** Es un cliente LLM  web, compatible API Ollama, interactua con los FM locales **(Phi-3.5 o Qwen 2.5)**. Lo desplegaremos usando Docker.

  
**RAG (*Retrieval-Augmented Generation*):** Técnica utilizada en IA para mejorar la precisión y confiabilidad los *LLM* (GPT, Gemini, etc.).Lo hace conectando el modelo a fuentes de datos externas y actualizadas antes de generar una respuesta.

**Docker Compose** es una herramienta desarrollada para definir y ejecutar aplicaciones Docker **multi-contenedor**.Mientras que el comando clásico de Docker **(`docker run`)** sirve para arrancar un contenedor de forma individual, Docker Compose te permite gestionar toda una arquitectura de servicios interconectados (por ejemplo, una base de datos, un servidor web, un backend y un panel de administración) de forma conjunta utilizando un único archivo de configuración estructurado en formato YAML.

****

## 2. Infografia.

![BGP WEIGTH](images/01Topologia.jpg)

****
### 1. Requisitos de Hardware Optimizados

Para mantener la eficiencia sin comprometer los recursos generales del servidor Proxmox:

* **CPU:** Mínimo **4 vCPUs** con soporte para instrucciones AVX2 (Intel Core de 8ª gen en adelante o AMD Ryzen/EPYC).  
* **Memoria RAM:** **12 GB a 16 GB** dedicados al FM (permite manejar con soltura el modelo de 3.8B/7B y ventanas de contexto grandes para logs de Rsyslog).  
* **Almacenamiento:** **60 GB en SSD/NVMe** (usando Thin Provisioning en Proxmox) para alojar el OS, los pesos de los SLMs y la persistencia de datos analizados.
* **Aceleración (Opcional):** GPU compatible (ej. NVIDIA con **6+ GB de VRAM**) mediante PCIe Passthrough si requieres alta velocidad en tiempo real.

### 2. Arquitectura Recomendada en Proxmox (VM vs LXC)

* **Elección Segura:** Se recomienda utilizar una **Máquina Virtual (VM)** con Ubuntu Server 24.04 LTS en lugar de un contenedor LXC.  
* **Justificación de Seguridad:** Las VMs ofrecen un aislamiento completo del kernel (*sandbox*), evitan vulnerabilidades de elevación de privilegios hacia el host Proxmox y simplifican la gestión de controladores y respaldos (*snapshots* nativos).

---

### 4. IMPLEMENTACION IA LOCAL Instalacion de OS (Ubuntu Server):

4.1) [Descargar Ubuntu Server 24.04 LTS](https://ubuntu.com/download/server?utm_source=gemini)

4.2) Crear la Máquina Virtual en Proxmox, con los siguientes parámetros: 

  * **Systema (Proxmox):**
Marca la casilla Qemu Agent:** Habilítala, para que Proxmox se comunique con la VM, permita apagarla/reiniciarla desde el panel, monitorear RAM y disco.

![IA Local Sistema](images/12requerimientosSystem.png)

   * **Disco:** 60 GB (SCSI/NVMe).
     
Ideal SSDs/NVMe y habilitar **Discard** (habilita TRIM/UNMAP), sin embargo, no la habilitamos por ser un disco mecanico.

![IA Local CPU](images/11requerimientosDisco.png)

   * **Cores:** 4 vCPUs (con tipo de CPU `host`).
 
 Implementacion minima CPU: La opción `host` le permite a la VM "heredar"  las instrucciones avanzadas del CPU físico (como AVX2 o instrucciones vectoriales).

![IA Local CPU](images/10requerimientosCPU.png)

   * **Memoria:** 12288 MB (12 GB), le coloque 16 RAM
   * 
![IA Local CPU](images/13requerimientosRAM.png)
 
   * **Red:** VirtIO (paravirtualizado).

![IA Local CPU](images/14requerimientosRED.png)
     

**Nota:** Una vez instalada la VM de Ubuntu debe tener acceso por SSH.
     
4.3) Instalación oficial y limpia de Ollama:

Ollama es el motor de inferencia local.

****

### 5. Instalacion de Motor de Inferencia local OLLAMA:

5.1)**Instalacion de OLLAMA:** Es la herramienta de software que  permitira correr el FM **(Phi-3.5 y/o Qwen 2.5)** en tu servidor VM UBUNTU.

```text
curl -fsSL https://ollama.com/install.sh | sh
```

Ollama es el motor de inferencia local (ejecuta los FM en la VM). Este comando cumple funciones críticas:

* **Automatiza la detección de hardware:** Analiza si la VM tiene CPU compatible o una tarjeta gráfica (GPU NVIDIA).
* **Descarga el binario oficial seguro:**  Descarga Ollama la versión binaria compilada.
* **Configura el servicio del sistema (Systemd):** Instala Ollama como un servicio (`systemctl`). Esto garantiza que si vm se reinicia, el motor de IA arrancará automáticamente y quedará escuchando en el puerto local (`11434`), listo para recibir las peticiones de tus scripts de Python.

![IA Instalacion Ollama](images/15Instalacionollama.png)

¡Instalación completada con éxito! El script finalizó correctamente y ya tienes Ollama operando como servicio de fondo en tu máquina virtual.

Puntos clave del resultado de la instalación:

* **Servicio activo:** Ollama ya está corriendo  en `127.0.0.1:11434`, listo para recibir peticiones locales.
* **Modo CPU:** `WARNING: No NVIDIA/AMD GPU detected. Ollama will run in CPU-only mode.`, es normal ya usaremos CPU la memoria RAM del host (sin tarjeta gráfica dedicada).

****

### 6. Descarga de los Modelos Optimizados para correr local


6.1) Descargar e instalar el primer FM **(Phi-3.5)**, ejecuta el siguiente comando en tu terminal:

```bash
ollama run phi3.5
```

* **Phi-3.5 Mini (3.8B):** Excelente velocidad y bajo consumo de RAM.
* **Qwen 2.5 (7B):** Muy superior en tareas de análisis sintáctico de código.

![IA Instalacion Ollama](images/16Instalacionfmphi35.png)

6.2) Descargar e instalar el segundo FM **(Qwen 2.5 )**, ejecuta el siguiente comando en tu terminal:

```text
ollama run qwen2.5:7b
```
****

### 7. Implementacion e Instalacion de cliente LLM (Open WebUI):

7.1) Instalar Docker y Docker Compose en la VM:

Si aún no tienes Docker instalado en tu Ubuntu Server, puedes instalarlo ejecutando los siguientes comandos en la terminal de tu VM:

```bash
# 1. Actualizar los paquetes del sistema
sudo apt update && sudo apt upgrade -y
```

7.2) Instalar Docker y Docker Compose en la VM:

```bash
# 2. Descargar e instalar Docker mediante el script oficial
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

7.3) Agregar tu usuario actual al grupo de Docker para no requerir 'sudo' en cada comando:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

7.4) Para verificar que quedó instalado correctamente:

```bash
docker --version
docker compose version
```

7.5) Desplegar el contenedor de Open WebUI:

Para conectar Open WebUI con tu instancia local de Ollama en el servidor, ejecuta el siguiente comando en tu terminal:

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

7.6) Una vez que el contenedor esté en marcha, puedes comprobar su estado ejecutando:

```bash
docker ps
```

7.7) Una vez que el contenedor esté en marcha, navegando usando el siguiente enlace:

```bash
http://10.0.30.59:3000
```
****

### 8. CONECTAR Cliente LLM (Open WebUI) con OLLAMA:

8.1) Para registrar OLLAMA para que interactue con Open WebUI:

En la misma ventana que muestra la imagen, haz clic en **"Manage Connections"** (o ve directamente a **Settings > Connections** en el menú lateral).

En la sección de Ollama API, cambia la URL de conexión. En lugar de `http://localhost:11434`, cámbiala por:

```text
http://10.0.30.59:11434
```
![Open WebUI](images/19Openwebgui.png)

8.2) Configurar Ollama para que escuche en todas las interfaces:

Para permitir que otros contenedores o servicios externos accedan a Ollama en el servidor, debes configurar el servicio systemd para que escuche en todas las interfaces de red.

Ejecuta el siguiente comando para editar la configuración del servicio, el cual añadira (Environment="OLLAMA_HOST=0.0.0.0:11434"):

```bash
sudo mkdir -p /etc/systemd/system/ollama.service.d && echo -e "[Service]\nEnvironment=\"OLLAMA_HOST=0.0.0.0:11434\"" | sudo tee /etc/systemd/system/ollama.service.d/override.conf
```

![Edit Ollama](images/20Ollamaservice.png)


8.3) Para aplicar los cambios, recarga el demonio de systemd y reinicia el servicio de Ollama con los siguientes comandos:

```bash
sudo systemctl daemon-reload
sudo systemctl restart ollama.service
```

![Edit Ollama](images/21Ollamaservice.png)

