#**Módulo 1: Fundamentos de Git y GitHub** 

???+ info "🎯 Objetivo del Módulo"
    Entender qué es Git, qué es GitHub y cómo se relacionan. Configurar el entorno local y remoto para empezar a trabajar en el proyecto "CollabApp".

---

##**📜 ¿Qué es el Control de Versiones?**

El Control de Versiones (VCS) es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo. Esto permite recuperar versiones específicas más adelante, comparar cambios, y colaborar de manera más eficiente.

>   **Piénsalo como:** Un historial detallado de "guardados" de tu proyecto, permitiéndote volver atrás o entender la evolución del mismo.

---

##**🆚 Git vs. GitHub: Entendiendo la Diferencia**

Es crucial distinguir entre estas dos herramientas que, aunque relacionadas, cumplen funciones diferentes:

*   **Git:**
    *   Es el **software de control de versiones distribuido** que se ejecuta en tu computadora.
    *   Permite rastrear cambios, crear ramas, fusionar trabajo, etc., de forma **local**.
    *   Es la herramienta fundamental para la gestión de versiones.

*   **GitHub:**
    *   Es una **plataforma web** que aloja repositorios Git en la nube.
    *   Facilita la **colaboración en equipo**, la revisión de código (Pull Requests), la gestión de proyectos (Issues), y sirve como un "backup" centralizado y accesible de tu código.
    *   Actúa como un **hub central** para los repositorios Git.

>   **En resumen:** `Git` es el motor, `GitHub` es la plataforma que potencia su uso colaborativo en la web.

---
???+ info "Git"

    === "**⚙️ Instalación y Configuración de Git**"

        Para empezar a usar Git, primero necesitas instalarlo y configurarlo.

        ???+ tip "Paso 1: Instalación de Git"
            Visita [https://git-scm.com/downloads](https://git-scm.com/downloads) y descarga el instalador adecuado para tu sistema operativo (Windows, macOS, Linux). Sigue las instrucciones del instalador.

        ???+ tip "Paso 2: Configuración Inicial de Identidad"
            Una vez instalado, abre una terminal (Git Bash en Windows, Terminal en macOS/Linux) y configura tu nombre de usuario y correo electrónico. Estos datos se asociarán a tus commits.
            ```bash
            git config --global user.name "Tu Nombre Completo"
            git config --global user.email "tu.email@ejemplo.com"
            ```
            *   La opción `--global` aplica esta configuración a todos tus proyectos Git.



    === "**Conceptos Clave de Git (Trabajo Local)**"

        Estos son los pilares del trabajo con Git en tu máquina:

        *   **Repositorio (`git init`):**
            *   Es la carpeta de tu proyecto que Git va a rastrear. Se crea ejecutando `git init` dentro de la carpeta del proyecto.
            *   *Caso CollabApp:* Ana crea una carpeta `CollabApp` y la inicializa:
                ```bash
                mkdir CollabApp
                cd CollabApp
                git init
                ```

        *   **Área de Staging (`git add`):**
            *   Antes de confirmar (hacer commit) los cambios, debes seleccionar explícitamente qué modificaciones quieres incluir en la próxima "foto" del proyecto.
            *   `git add <nombre_archivo>`: Añade un archivo específico al staging area.
            *   `git add .`: Añade todos los archivos modificados o nuevos en el directorio actual y subdirectorios.
            *   *Caso CollabApp:* Ana crea `README.md` y lo añade al staging:
                ```bash
                echo "# CollabApp - Herramienta de Gestión de Tareas" > README.md
                git add README.md
                ```

        *   **Confirmaciones / Commits (`git commit`):**
            *   Es el acto de guardar los cambios preparados (staged) en el historial del repositorio. Cada commit es una "instantánea" del proyecto en un momento dado.
            *   Es crucial escribir un **mensaje de commit claro y descriptivo**.
                ```bash
                git commit -m "feat: Inicializar proyecto con README básico"
                ```
            !!! note "Convenciones de Mensajes de Commit"
                Es una buena práctica usar prefijos para indicar el tipo de cambio (ej. `feat:` para nueva funcionalidad, `fix:` para corrección, `docs:` para documentación, `style:`, `refactor:`, `test:`, `chore:` para mantenimiento).

        *   **Historial (`git log`):**
            *   Muestra la lista de commits realizados, quién los hizo, cuándo y con qué mensaje.
                ```bash
                git log
                ```

        *   **Estado (`git status`):**
            *   Muestra el estado actual de tus archivos: modificados pero no en staging, en staging, sin rastrear, o si la rama actual está al día con la remota. Es un comando que usarás constantemente.
                ```bash
                git status
                ```


???+ info "**Creación de una Cuenta en GitHub**"

    Dirígete a [https://github.com](https://github.com) y sigue el proceso de registro ("Sign up") para crear tu cuenta personal.

    === "Creación de un Repositorio Remoto en GitHub"

        Una vez con tu cuenta, puedes crear repositorios para alojar tus proyectos.

        **Caso CollabApp:** Ana, desde su cuenta de GitHub:

            1.Clic en el icono "+" (esquina superior derecha) ➡️ "New repository".
            2.**Repository name:** `CollabApp`
            3. **Description:** (Opcional) "Proyecto de herramienta de gestión de tareas."
            4.  Elige entre **Public** o **Private**. (Para CollabApp, eligen Privado).
            5.  **Importante:** *No* selecciones "Initialize this repository with a README", ".gitignore", o "license" si ya tienes un proyecto local existente que quieres subir.
            6.  Clic en "Create repository".

    === "Conectar Repositorio Local con Remoto y Subir Cambios"

        Ahora, vincularemos el repositorio local de Ana con el que acaba de crear en GitHub.

        ???+ abstract "Pasos para Conectar y Subir"
            1.  **Añadir el Remoto:**
                GitHub te proporcionará una URL para tu repositorio remoto (ej. `https://github.com/TuUsuario/CollabApp.git`). Usa esta URL para "registrar" el remoto en tu Git local:
                ```bash
                    # (Dentro de la carpeta local CollabApp)
                    git remote add origin https://github.com/TuUsuario/CollabApp.git
                ```
            **`origin`** es el nombre por defecto y más común para el repositorio remoto principal.

            2.  **Verificar Remotos Configurados:**
                ```bash
                    git remote -v
                ```
                Esto mostrará las URLs para `fetch` (traer) y `push` (enviar) de `origin`.

            3.  **(Opcional pero Recomendado) Renombrar Rama Principal a `main`:**
                Si tu rama principal local se llama `master` (común en versiones antiguas de Git), es buena práctica renombrarla a `main`:
                ```bash
                    git branch -M main
                ```

            4.  **Empujar (Push) los Commits Locales al Remoto:**
                La primera vez que empujas a un nuevo repositorio o una nueva rama, necesitas especificar a dónde van los cambios y establecer un seguimiento (upstream):
                ```bash
                    git push -u origin main
                ```
                *   `-u` (o `--set-upstream`) vincula tu rama `main` local con la rama `main` en `origin`.
                *   En pushes subsecuentes desde esta rama, solo necesitarás `git push`.
  
    === "Clonar un Repositorio Remoto (`git clone`)"

        Para que otros miembros del equipo (Bruno y Carla) puedan trabajar en "CollabApp", necesitan obtener una copia del proyecto.

        *   *Caso CollabApp:* Bruno y Carla ejecutan en sus terminales:
            ```bash
               git clone https://github.com/UsuarioDeAna/CollabApp.git
            ```
        *   Esto crea una carpeta `CollabApp` en sus máquinas con todo el proyecto.
        *   Automáticamente configura el remoto `origin` para apuntar al repositorio de GitHub desde donde se clonó.

    === "Sincronizar Cambios: `push` y `pull`"

        La colaboración implica enviar y recibir cambios:

        *   **`git push`:**
            *   Envía tus commits locales (que están en tu máquina pero no en GitHub) al repositorio remoto.
            *   *Ejemplo:* Después de hacer nuevos commits, Ana ejecuta `git push` para compartir su progreso.

        *   **`git pull`:**
            *   Trae los cambios del repositorio remoto a tu copia local y trata de fusionarlos con tu trabajo actual.
            *   Es una combinación de `git fetch` (que descarga los cambios remotos) y `git merge` (que los integra).
            *   *Ejemplo:* Antes de empezar a trabajar, o para obtener los cambios de Ana, Bruno ejecuta `git pull origin main`.
            
    === "Archivos Esenciales: `.gitignore` y `README.md`"

        Dos archivos son cruciales para la buena gestión de un repositorio:

        *   **`.gitignore`:**
            *   Un archivo de texto plano llamado `.gitignore` (con el punto al inicio).
            *   Especifica archivos y carpetas que Git debe **ignorar** y no rastrear.
            *   Esencial para evitar subir archivos generados, dependencias (ej. `node_modules/`), archivos de configuración del IDE, o datos sensibles.
            *   *Ejemplo de contenido para `.gitignore` en CollabApp:*
                ```gitignore
                    # Dependencias
                    node_modules/
                    vendor/

                    # Archivos de entorno (¡Nunca subir secretos!)
                    .env
                    *.env.local

                    # Logs
                    *.log
                    npm-debug.log*
                    yarn-debug.log*
                    yarn-error.log*

                    # Archivos de build/distribución
                    dist/
                    build/

                    # Archivos de sistema operativo
                    .DS_Store
                    Thumbs.db
                ```
            *   **Importante:** Crea, añade y commitea tu `.gitignore` al repositorio.
                ```bash
                    # Crear el archivo .gitignore con el contenido deseado
                    git add .gitignore
                    git commit -m "chore: Añadir archivo .gitignore con patrones básicos"
                    git push
                ```

        *   **`README.md`:**
            *   Es la "portada" de tu proyecto en GitHub. Escrito en formato [Markdown](https://www.markdownguide.org/basic-syntax/).
            *   Debe proporcionar una descripción clara del proyecto: qué hace, cómo instalarlo, cómo usarlo, y (eventualmente) cómo contribuir.
            *   Es lo primero que un visitante (o un nuevo miembro del equipo) verá.



## 🛠️ Práctica Sugerida

???+ exercise "Ejercicio 1: Configuración y Primer Repositorio Individual"
    1.  Asegúrate de que Git esté instalado y configurado con tu `user.name` y `user.email`.
    2.  Crea una cuenta en GitHub si no la tienes.
    3.  En GitHub, crea un nuevo repositorio privado llamado `mi-primer-proyecto-colaborativo` (sin inicializarlo con archivos).
    4.  En tu máquina local, crea una carpeta con el mismo nombre, entra en ella e inicializa un repositorio Git (`git init`).
    5.  Crea un archivo `README.md` con una breve descripción de lo que harías en un proyecto colaborativo.
    6.  Crea un archivo `.gitignore` e incluye al menos `*.log` y una carpeta como `temp/` o `cache/`.
    7.  Añade ambos archivos al staging area (`git add .`).
    8.  Realiza un commit con un mensaje descriptivo (ej. `feat: Configuración inicial del proyecto con README y gitignore`).
    9.  Conecta tu repositorio local con el remoto de GitHub (`git remote add origin <URL_DE_TU_REPO>`).
    10. (Si es necesario) Renombra tu rama principal a `main` (`git branch -M main`).
    11. Empuja tus cambios a GitHub (`git push -u origin main`).
    12. Verifica en GitHub que tus archivos están allí.

???+ exercise "Ejercicio 2 (Opcional, en Pareja): Simulación Básica de Colaboración"
    *   **Persona A:**
        1.  Crea un nuevo repositorio privado en GitHub (ej. `CollabApp-Test`).
        2.  Lo clona a su máquina.
        3.  Añade un `README.md` simple y un `.gitignore`. Hace commit y push.
        4.  Invita a la Persona B como colaboradora al repositorio en GitHub (Settings > Manage access > Invite a collaborator).
    *   **Persona B:**
        1.  Acepta la invitación.
        2.  Clona el repositorio `CollabApp-Test` a su máquina.
        3.  Modifica el `README.md` (añade una línea o cambia algo).
        4.  Hace `git add README.md`, `git commit -m "docs: Actualización del README por Persona B"`, y `git push`.
    *   **Persona A:**
        1.  En su repositorio local, ejecuta `git pull origin main`.
        2.  Verifica que el `README.md` ahora incluye los cambios de la Persona B.

---

!!! success "✅ Puntos Clave del Fundamentos"
    *   Diferencia entre **Git (local)** y **GitHub (remoto/plataforma)**.
    *   Configuración básica de Git (`user.name`, `user.email`).
    *   Flujo de trabajo local fundamental: `init` ➡️ `add` ➡️ `commit`.
    *   Conexión con GitHub: `remote add`, `push`.
    *   Obtención de proyectos: `clone`.
    *   Sincronización: `pull` (para obtener cambios), `push` (para enviar cambios).
    *   Importancia y uso básico de `.gitignore` y `README.md`.

---

Ahora estás listo para el siguiente paso: aprender sobre **ramas (branches)**, que son esenciales para el trabajo paralelo y colaborativo.