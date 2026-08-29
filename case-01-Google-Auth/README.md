# Configurar Credenciales de Google en n8n utilizando **OAuth 2.0**

Conocimientos previos: [Set up Google Credentials in n8n in 5 minutes (2025)](https://www.youtube.com/watch?v=3Ai1EPznlAc)

![Infografia](images/Infografia.jpg)

La consola de Google Cloud (**Google Cloud Console**) es el panel de control web que ofrece Google para administrar y gestionar todos los servicios de su plataforma de computación en la nube, conocida como **Google Cloud Platform (GCP)**.

IMPORTANTE:

Hay 2 maneras de autenticacion **Clave de API**  y **OAuth 2.0**:

La diferencia principal radica en qué tipo de recursos controlan y cómo interactúan con tus datos personales:

1) **Clave de API** (Google AI Studio / la de tu imagen): Es una contraseña simple y directa pensada para consumir servicios públicos o modelos de inteligencia artificial (como Gemini). No sabe quién eres tú como persona ni accede a tus archivos personales; solo autoriza al software a usar una herramienta o cuota de IA dentro de un proyecto.

2) **OAuth 2.0** (el que estamos configurando para n8n): Es un protocolo de autorización segura diseñado para acceder a datos privados de usuario (tus documentos de Google Drive, tus correos de Gmail, tus hojas de cálculo, etc.). Requiere que tú (el usuario) inicies sesión explícitamente y des el consentimiento mediante una ventana de autorización (*Sign in with Google*) para que la aplicación externa pueda actuar en tu nombre.

**En resumen:** la Clave de API es para consumir servicios generales o de IA, mientras que el OAuth es obligatorio cuando n8n necesita entrar a tus aplicaciones personales de Google.

**Para crear Clave de API** 

1. Abre una nueva pestaña en tu navegador y entra a: [aistudio.google.com](https://aistudio.google.com)
2. Inicia sesión con la misma cuenta de Google que ya estás usando.
3. En la esquina superior izquierda o en el menú principal, haz clic en el botón que dice **"Get API key"** (Obtener clave de API).
4. Haz clic en **"Create API key in new project"** (Crear clave de API en un proyecto nuevo).
5. ¡Listo! Te aparecerá tu llave secreta en pantalla de forma inmediata. Cópiala.


## Guía Paso a Paso en 5 Minutos (2025) utilizando **OAuth 2.0**

### 🛠️ Fase 1: Prerrequisitos en Google Cloud Platform (GCP)

#### Crear un Proyecto en Google Cloud
1. - Entra a Google Cloud e inicia el proceso para crear un nuevo proyecto.

    https://console.cloud.google.com/

- Asígnale un nombre (por ejemplo, `demo`) y haz clic en **Crear**.
- Asegúrate de seleccionar el proyecto recién creado en la esquina superior de la consola.

2. - Configurar la Pantalla de Consentimiento OAuth

- Seleccionar el proyecto:

  ![Aoth](images/0Seleccionarproyecto.png)

- En la barra de busqueda escoger (APIs y servicios habilitados):

 ![Aoth](images/01SeleccionarAPIsyservicios.png)

- Seleccionar pantalla de consentimiento (En el menú de navegación de GCP, ve a APIs y servicios > Pantalla de consentimiento OAuth):

 ![Aoth](images/01Seleccionarpantalladeconsentimiento.png)

- Seleccionar informacion de la marca (llenar toda la informacion):

  ![Aoth](images/01Seleccionarinformaciondemarca.png)

- Seleccionar clientes:

   ![Aoth](images/01Seleccionarclientes.png)

- Crear clientes:

 ![Aoth](images/01CrearclienteOAuth.png)

 - Nombre de cliente y click en CREAR:

 ![Aoth](images/01nombreclientes.png)

 - Ya queda creado el OUATH:

[Set up Google Credentials in n8n in 5 minutes (2025)](https://www.youtube.com/watch?v=3Ai1EPznlAc)

 ![Aoth](images/01OAuthcreado.png)

 Para acceder a la configuracion usar el siguiente enlace:

 [Valores de OUATH ](https://console.cloud.google.com/auth/clients?project=linen-surface-507011-b0)

3. - Añadir Usuarios de Prueba

- En la sección de usuarios de prueba, agrega las cuentas de correo electrónico (la tuya) que tendrán permiso para realizar las pruebas y acceder a Google Drive, Docs y Gmail.
- Haz clic en **Guardar y continuar**.


 ### 🛠️ Fase 1: Prerrequisitos en Google Cloud Platform (GCP)
