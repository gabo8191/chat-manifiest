# Guía de Pruebas para Manifiestos de PWA

Este directorio contiene diferentes versiones del `manifest.json` para probar varias características de las Progressive Web Apps.

## Proceso Básico de Prueba

1.  **Instala la PWA**: Asegúrate de que la PWA no esté instalada en tu dispositivo de prueba (móvil o escritorio).
2.  **Copia el Manifiesto**: Elige el manifiesto que deseas probar (ej. `manifest-permisos.json`) y cópialo a la raíz del proyecto, renombrándolo a `manifest.json`.
    ```bash
    cp manifests/manifest-permisos.json manifest.json
    ```
3.  **Recarga y Valida**: Abre la aplicación en tu navegador, ve a las Herramientas de Desarrollador (F12) -> `Application` -> `Manifest`. Asegúrate de que el navegador lea el nuevo manifiesto correctamente.
4.  **Instala y Prueba**: Instala la PWA en tu dispositivo y sigue las instrucciones de validación específicas para cada manifiesto a continuación.
5.  **Limpia**: Desinstala la PWA antes de probar el siguiente manifiesto para asegurar un entorno limpio.

---

## Guía de Validación por Manifiesto

### 1. `manifest-metadata.json`

-   **Qué prueba**: La identidad y apariencia de la PWA durante la instalación.
-   **Cómo validar**:
    -   Al iniciar el proceso de instalación, el diálogo debería mostrar el nombre "Chat para Héroes - Edición Metadatos".
    -   Las capturas de pantalla definidas en el manifiesto deberían aparecer en el diálogo de instalación (soporte varía según el SO).
    -   Una vez instalada, el ícono en la pantalla de inicio/escritorio debería usar la versión "maskable" para adaptarse a la forma del sistema (especialmente visible en Android).
    -   El nombre debajo del ícono debería ser "Chat Meta".

### 2. `manifest-permisos.json`

-   **Qué prueba**: La integración de la PWA con otras aplicaciones y el sistema operativo.
-   **Cómo validar** (requiere un navegador/SO compatible, como Chrome/Edge en escritorio o Android):
    -   **`share_target`**: Abre otra aplicación (ej. galería de fotos, navegador web) y usa la función "Compartir". Tu PWA "Chat Caps" debería aparecer en la lista de aplicaciones con las que puedes compartir. Al seleccionarla, la PWA debería abrirse y recibir los datos.
    -   **`file_handlers`**: En el explorador de archivos de tu sistema operativo, haz clic derecho sobre un archivo `.txt` o `.jpg`. En el menú "Abrir con...", tu PWA "Chat Caps" debería ser una de las opciones.
    -   **`protocol_handlers`**: Escribe `web+chathero://info` en la barra de direcciones de tu navegador (o crea un enlace `<a>` con ese `href`). El navegador debería preguntarte si quieres abrir el enlace con la aplicación "Chat Caps".

### 3. `manifest-ventana.json`

-   **Qué prueba**: El comportamiento y la apariencia de la ventana de la PWA.
-   **Cómo validar**:
    -   **`display_override`**: En un sistema operativo de escritorio (Windows, macOS, Linux con un navegador compatible), la PWA debería abrirse en una ventana donde la barra de título del sistema está oculta, permitiendo que el contenido web se dibuje en esa área (Window Controls Overlay).
    -   **`launch_handler`**: Con la PWA ya abierta, intenta volver a abrirla (por ejemplo, haciendo clic en su ícono de nuevo o desde un enlace). En lugar de abrir una nueva ventana, la ventana existente debería ponerse en foco.
    -   **`theme_color`**: La barra de título de la ventana de la PWA debería tener el color azul oscuro (`#2980b9`) definido.

### 4. `manifest-desarrollador.json`

-   **Qué prueba**: Funciones orientadas a la distribución y accesos directos para el usuario.
-   **Cómo validar**:
    -   **`shortcuts`**: Una vez instalada la PWA, haz un clic largo (en móvil) o un clic derecho (en escritorio) sobre el ícono de la aplicación. Debería aparecer un menú contextual con las opciones "Crear nuevo mensaje" y "Ver mis contactos". Al hacer clic en ellas, la PWA debería abrirse en la URL especificada.
    -   **`related_applications`**: Esta es una sugerencia para el navegador. Su validación principal es confirmar que el manifiesto sigue siendo válido. En algunos casos, el navegador podría mostrar una notificación sugiriendo la instalación de la app nativa si está disponible en la tienda.

### 5. `manifest-otros.json`

-   **Qué prueba**: Características experimentales o menos comunes.
-   **Cómo validar**:
    -   **`note_taking`**: En un dispositivo con un asistente de voz compatible (como Android con el Asistente de Google), prueba un comando como: "Ok Google, toma una nota con Chat Extra". El asistente podría iniciar tu PWA.
    -   **`edge_side_panel`**: Si estás usando Microsoft Edge en escritorio, revisa si puedes abrir la PWA en el panel lateral del navegador.
    -   **`scope_extensions`**: Esta es una característica avanzada que requiere configuración de servidor y es difícil de validar localmente sin los dominios asociados. La validación principal es que el manifiesto sea aceptado por el navegador.
