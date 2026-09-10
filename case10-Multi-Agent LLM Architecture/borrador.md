## 1. Arquitectura de LLM Multi-Agente (Arquitectura de LLMs Multi-Agente):

![IA Local CPU](images/00Arquitectura.jpg)

**(Arquitectura de LLMs Multi-Agente):** Sistemas donde múltiples agentes de IA especializados colaboran para resolver tareas complejas que un solo prompt o modelo monolítico no podría manejar eficientemente.

**Orquestación Jerárquica o Supervisor-Trabajador:** Es el patrón de diseño exacto de control. Tienes un agente central (el FM o "Router") como arquitecto jefe o director de orquesta, el cual analiza la tarea y delega subtareas a los agentes especializados en los bordes.

**Enrutamiento Dinámico de Tareas (Dynamic Task Routing) y Role Prompting:**

> **Definición:** Los pasos 1 y 4 combinan la técnica de asignación de roles estrictos (*Role Prompting*) con la capacidad del sistema de rutear inteligentemente la petición del usuario hacia el dominio técnico correcto.

> **Nota técnica:** Las arquitecturas de LLM multi-agente descomponen tareas monolíticas complejas en roles de agentes especializados y cooperativos (por ejemplo, orquestadores, desarrolladores, revisores) para mejorar la precisión, la profundidad de razonamiento y la modularidad.
---

### Componentes Clave de los Sistemas Multi-Agente

* **Orquestador / Enrutador:** Coordina el flujo de trabajo, gestiona la distribución de tareas y determina qué agente especializado debe encargarse de una subtarea determinada.
* **Agentes Especializados:** Instancias de LLM configuradas con mensajes, herramientas y restricciones distintivas adaptadas a dominios específicos (por ejemplo, generación de código, auditoría de seguridad, documentación).
* **Contexto / Estado Compartido:** Una memoria centralizada o bus de comunicación (como un patrón de pizarra o un intermediario de mensajes) que permite a los agentes compartir resultados intermedios y mantener la conciencia situacional.
