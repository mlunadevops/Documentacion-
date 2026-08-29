# Cómo Configurar Credenciales de Google en n8n

Conocimientos previos:

La consola de Google Cloud (**Google Cloud Console**) es el panel de control web que ofrece Google para administrar y gestionar todos los servicios de su plataforma de computación en la nube, conocida como **Google Cloud Platform (GCP)**.

Fuente (Set up Google Credentials in n8n in 5 minutes (2025)): https://www.youtube.com/watch?v=3Ai1EPznlAc

## Guía Paso a Paso en 5 Minutos (2025)

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

 ![Aoth](images/01OAuthcreado.png)

