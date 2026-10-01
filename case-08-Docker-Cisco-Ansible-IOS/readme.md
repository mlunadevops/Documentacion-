# Configuración de Entorno Docker para Ansible (Cisco IOS)

Esta guía detalla los pasos y comandos ejecutados en Windows PowerShell para desplegar y configurar un contenedor Docker especializado como controlador de Ansible, listo para administrar dispositivos de red Cisco IOS.

---

### 1. Ubicarse en el directorio de trabajo
Cambiamos a la ruta local en tu equipo donde se almacenarán los archivos de configuración de Docker.

```powershell
Set-Location "G:\Mi unidad\DockerIOS"
```

---

### 2. Crear el archivo de configuración `Dockerfile`
Se genera un archivo vacío que servirá como la receta principal para construir la imagen personalizada.

```powershell
New-Item -ItemType File -Name Dockerfile
```

---

### 3. Escribir el contenido del `Dockerfile`
Se define la imagen base de Python (versión ligera `slim`), se instalan las herramientas esenciales del sistema operativo (Git, cliente SSH, utilidades de red) y se agregan las librerías de Python junto con la colección oficial de Ansible para Cisco IOS.

```powershell
Set-Content -Path "Dockerfile" -Value @"
FROM python:3.11-slim

RUN apt-get update && apt-get install -y \
    git \
    ssh \
    iputils-ping \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir ansible paramiko netaddr

RUN ansible-galaxy collection install cisco.ios

WORKDIR /workspace

CMD ["bash"]
"@
```

---

### 4. Construir la imagen de Docker
Mediante el comando `build`, Docker procesa el `Dockerfile`, descarga las dependencias necesarias y empaqueta la imagen personalizada bajo el nombre `ansible-cisco-lab`.

```powershell
docker build -t ansible-cisco-lab .
```

---

### 5. Ejecutar el contenedor interactivo
Finalmente, se inicia y se accede al contenedor en modo interactivo (`-it`) asignándole el nombre `ansible-controller`, dejándote posicionado directamente en la ruta de trabajo `/workspace#`.

```powershell
docker run -it --name ansible-controller ansible-cisco-lab
```
