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

Por lo tanto, el API REST utiliza el protocolo **HTTP** como canal de comunicacion, **JSON** como lenguaje/formato para conectar al cliente con el servidor y el metodo (verbo) son las instrucciones y respuestas que se intercam.

En este contexto, un método (también conocido como verbo HTTP) es la acción explícita que le indica al servidor qué es lo que el cliente quiere hacer con el recurso.
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

## 2. Topologia e Infografia

The topology consists of four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

![GNS3 MCP Install](images/10pipinstallgns3mcp.png)

 four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

## 3. IMPLEMENTACION:

**Router A (RTA - AS 100):**

```text
! 
router bgp 100
!
```

### 4. BGP Configuration:
