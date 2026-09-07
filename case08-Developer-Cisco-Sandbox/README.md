# TECHNICAL LOG & DEVELOPER CISCO SANDBOXES

## Traffic Manipulation via the Weight Attribute
**CCNP Miguelangel Luna**

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |
| **02** | [Packet Tracert & VS CODE](./case-02-PT-MCP-VS-Code/) | Conecta Packet Tracert con MCP |


[Developer Cisco Sandbox](https://developer.cisco.com/site/sandbox/)

## 1. Introduction and Theoretical Framework

Para comenzar desde cero siendo novato, el mayor error es intentar configurar una red compleja de inmediato. Lo ideal es ir paso a paso, combinando conceptos básicos de programación con la infraestructura de Cisco.

Aquí tienes una ruta de aprendizaje práctica con las primeras cosas que puedes realizar, ordenadas de lo más simple a lo más avanzado:

### 1. Tus primeros pasos (Sin tocar redes aún)
Antes de interactuar con un router, necesitas aprender a hablar el idioma de las plataformas modernas (las APIs).

- **Hacer tu primera consulta con Postman:** Instala la herramienta gratuita Postman. Utiliza un *sandbox* "Always-on" (como el de Cisco Catalyst Center) para pedirle al sistema que te devuelva una lista de todos los equipos conectados. Verás la respuesta en un formato de texto limpio llamado JSON.
- **Crear un Bot básico para Cisco Webex:** Es el proyecto para novatos más divertido. Puedes programar un bot sencillo en Webex para que salude, envíe un reporte automático o responda a comandos específicos en un chat.

### 2. Automatización básica con Python
Python es el rey de la automatización de redes. Una vez que entiendas las variables y los bucles básicos, puedes hacer esto:

- **Pedir información a un router con un script:** Escribe un código de solo 10 líneas en Python para conectarte a un router virtual en el Sandbox y traer la información de su modelo, versión de software y tiempo encendido.
- **Cambiar el nombre de un equipo mediante código:** En lugar de entrar a la consola negra tradicional del router, haz que tu script de Python cambie el nombre del equipo (*Hostname*) de forma automática.

### 3. Configuración masiva (El verdadero poder)
Cuando domines lo anterior, estarás listo para simular el trabajo de un ingeniero del día a día:

- **Encender o apagar interfaces de red:** Imagina que tienes que apagar 20 puertos de un *switch* por seguridad. En lugar de hacerlo uno por uno, harás que un script de Python o una herramienta llamada Ansible los apague todos en un solo segundo.
- **Crear redes virtuales (VLANs) automáticamente:** Podrás escribir un archivo de texto donde definas qué redes necesitas (ej. VLAN 10 - Ventas, VLAN 20 - RRHH) y enviarlo al sandbox para que se configuren solas.

---

### 🚀 Tu punto de partida hoy mismo
Para no abrumarte, te sugiero empezar con el curso gratuito e interactivo de la misma plataforma: **Cisco DevNet Learning Labs**. Son tutoriales guiados que te dan el código hecho para que solo tengas que copiar, pegar, entender cómo funciona y ver el resultado en el Sandbox.


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
