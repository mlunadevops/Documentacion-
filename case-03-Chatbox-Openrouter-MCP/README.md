# TECHNICAL LOG & CHATBOX OPENROUTER MCP

## Traffic Manipulation via the Weight Attribute
**CCNP Miguelangel Luna**

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |
| **02** | [Packet Tracert & VS CODE](./case-02-PT-MCP-VS-Code/) | Conecta Packet Tracert con MCP |


[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework

El Model Context Protocol (MCP) utiliza una arquitectura cliente-servidor 🔌 diseñada para estandarizar cómo los modelos de IA interactúan con entornos locales y remotos.

(Claude Desktop, VS CODE con Github Copilot, etc), TA

Los tres componentes fundamentales son:

- **🤖 Cliente de IA (Cliente LLM):** Aplicación (*frontend*)** instalada en PC que se comunica con el modelo fundacional, es decir, es la interfaz gráfica  instalada en la PC, Smartphone, etc. Como ejemplo el claude desktop se instala en tu PC y te permite comunicarte con el modelo de lenguaje de Anthropic (Claude) que corre en sus servidores **(*backend*)**.

Hay 2 tipos de clientes LLM:

1) **Clientes oficiales de Grandes Modelos:**  Son aplicaciones creadas por las mismas empresas dueñas de la IA. Ejemplos:

1.1) GitHub Copilot

1.2) Claude Desktop

1.3) ChatGPT Desktop App
   
2) **Clientes Universales / Agnósticos:**  Estos programas no tienen una IA propia. Son interfaces vacías que te permiten ingresar tus propias API Keys para conectarte al modelo que tú quieras, ejemplos (Claude, GPT, DeepSeek, Llama).

2.1) Chatbox: Uno de los clientes de escritorio más populares y limpios. Es multiplataforma (Windows, Mac, Linux, móviles) y te permite cambiar de proveedor de IA con un solo clic.
   
2.2) Cline en VS CODE.
   
2.3) Jan: Un cliente de escritorio excelente porque funciona de dos formas: puede conectarse a IA en la nube mediante API, o puede descargar modelos de código abierto para correr 100% en local en tu computadora (sin internet).

2.4) LibreChat: Un cliente web que clona exactamente la interfaz de ChatGPT, pero te permite conectar las API de Anthropic, OpenAI y otros proveedores en un solo lugar.

En el caso de las practicas, vamos a usar el VS CODE con una extension 


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
