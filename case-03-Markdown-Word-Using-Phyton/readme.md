# Script de Python para generar el archivo Word (.docx)

1) Asegúrate de tener instalado `python-docx` (si no lo tienes, instálalo con `pip install python-docx`).

2) Guarda el siguiente código en un archivo llamado `generar_word.py` y ejecútalo (`python generar_word.py`):

```text
from docx import Document

# Crear documento
doc = Document()

# Título principal
doc.add_heading('Manual de Integración: Happy Path de MCP con Cisco Packet Tracer y VS Code', level=0)

# Fase 1
doc.add_heading('Fase 1: Configuración del Backend y Seguridad', level=1)

doc.add_heading('1. Clonación del Repositorio Local', level=2)
doc.add_paragraph('Abre una terminal de PowerShell y clona el repositorio oficial del proyecto en tu máquina local:')
doc.add_paragraph('cd ~\ngit clone https://github.com/Mats2208/MCP-Packet-Tracer.git', style='Intense Quote')

doc.add_heading('2. Creación del Entorno Virtual e Instalación', level=2)
doc.add_paragraph('Entra a la carpeta del proyecto, crea y activa tu entorno virtual de Python, y procede a instalar el paquete en modo editable:')
doc.add_paragraph('cd MCP-Packet-Tracer\npython -m venv venv\n.\\venv\\Scripts\\Activate.ps1\npython -m pip install --upgrade pip\npip install -e .', style='Intense Quote')

doc.add_heading('3. Ejecución del Servidor MCP', level=2)
doc.add_paragraph('Inicia el servidor basado en Uvicorn para que quede escuchando las peticiones locales:')
doc.add_paragraph('python -m packet_tracer_mcp', style='Intense Quote')
doc.add_paragraph('(El servidor se mantendrá activo en http://127.0.0.1:39000).')

doc.add_heading('4. Generación y Creación del Token de Seguridad', level=2)
doc.add_paragraph('Si intentas iniciar sin el token, verás un error en los registros de Packet Tracer.')
doc.add_paragraph('[Insertar imagen: image_d22713.png]')
doc.add_paragraph('Para solucionarlo, crea manualmente la ruta y el archivo bridge_token ejecutando:')
doc.add_paragraph('New-Item -ItemType Directory -Force -Path "C:\\Users\\Admin\\AppData\\Local\\packet-tracer-mcp"\nSet-Content -Path "C:\\Users\\Admin\\AppData\\Local\\packet-tracer-mcp\\bridge_token" -Value "token123"', style='Intense Quote')
doc.add_paragraph('Al verificar en el Explorador de archivos, la estructura lucirá con su carpeta interna bridge e incluirá:')
doc.add_paragraph('[Insertar imagen: image_d22b69.png]')
doc.add_paragraph('[Insertar imagen: image_d22ab4.png]')
doc.add_paragraph('[Insertar imagen: image_d22b0e.png]')

# Fase 2
doc.add_heading('Fase 2: Configuración del Módulo en Cisco Packet Tracer', level=1)

doc.add_heading('5. Descarga de la Extensión Oficial', level=2)
doc.add_paragraph('Dirígete al repositorio de GitHub y descarga el archivo de la extensión de Packet Tracer (.pts) correspondiente a la versión oficial requerida (V5.2.pts).')
doc.add_paragraph('[Insertar imagen: 05CiscoPTConfigscripts.png]')

doc.add_heading('6. Carga del Módulo en el Entorno de Packet Tracer', level=2)
doc.add_paragraph('Abre Cisco Packet Tracer, ve al menú de configuración de scripts de extensión (Configure PT Script Modules).')
doc.add_paragraph('[Insertar imagen: 02CiscoPTConfigscripts.png]')
doc.add_paragraph('Haz clic en el botón Add para abrir el explorador de archivos de Windows y seleccionar el archivo .pts.')
doc.add_paragraph('[Insertar imagen: 03CiscoPTConfigscripts.png]')
doc.add_paragraph('[Insertar imagen: 04CiscoPTConfigscripts.png]')

doc.add_heading('7. Verificación del Módulo MCP-BUILDER', level=2)
doc.add_paragraph('Una vez cargado, el módulo aparecerá integrado en la lista bajo el nombre de MCP-BUILDER (com.matsoto.mcpbuilder).')
doc.add_paragraph('[Insertar imagen: 06CiscoPTConfigscripts.png]')
doc.add_paragraph('Selecciónalo y haz clic en el botón Start para ponerlo en marcha.')
doc.add_paragraph('[Insertar imagen: 07CiscoPTConfigscripts.png]')

doc.add_heading('8. Uso del Editor de Scripts y Autenticación Exitosa', level=2)
doc.add_paragraph('Se abrirá la interfaz del editor de código del MCP-BUILDER con las plantillas de comandos de ejemplo.')
doc.add_paragraph('[Insertar imagen: 08CiscoPTConfigscripts.png]')
doc.add_paragraph('Al validar la terminal del panel de control con el token creado, obtendrás el mensaje de éxito que confirma que el puente está en línea.')
doc.add_paragraph('[Insertar imagen: 17CiscoPTcontinue.png]')

# Fase 3
doc.add_heading('Fase 3: Integración de MCP en VS Code', level=1)

doc.add_heading('9. Exploración del Marketplace de Servidores MCP', level=2)
doc.add_paragraph('Abre Visual Studio Code y dirígete al panel de extensiones para ubicar la sección de MCP Servers.')
doc.add_paragraph('[Insertar imagen: 09CiscoPTmcpservers.png]')

doc.add_heading('10. Acceso a las Preferencias de Usuario', level=2)
doc.add_paragraph('Abre la paleta de comandos (Ctrl + Shift + P), escribe preferences y selecciona la opción de gestión de preferencias o ajustes.')
doc.add_paragraph('[Insertar imagen: 10CiscoPTManagextension.png]')

doc.add_heading('11. Activación de la Galería mediante Configuración JSON', level=2)
doc.add_paragraph('Asegúrate de que tu archivo de configuración de usuario (settings.json) contenga la propiedad que habilita el marketplace de chat para las extensiones MCP:')
doc.add_paragraph('{\n    "chat.mcp.gallery.enabled": true\n}', style='Intense Quote')
doc.add_paragraph('[Insertar imagen: 11CiscoPTManagextension.png]')

# Guardar documento
doc.save('Happy_Path_MCP_Cisco_Packet_Tracer.docx')
print("¡Archivo Word generado con éxito como 'Happy_Path_MCP_Cisco_Packet_Tracer.docx'!")
```

3) Para ejecutar el script correctamente, abre tu terminal o consola en la carpeta donde guardaste el archivo (generar_word.py) y escribe el siguiente comando:

```text
python generar_word.py
```


