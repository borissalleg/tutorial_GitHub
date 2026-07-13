# Módulo 3: Pull Requests (PRs) – El Corazón de la Colaboración y Revisión

???+ info "🎯 Objetivo del Módulo"
    Entender y utilizar los Pull Requests (PRs) como el mecanismo central en GitHub para proponer, discutir, revisar e integrar cambios de una rama de funcionalidad (o corrección) a la rama principal (ej. `main`). Este es el pilar de la revisión de código en el proyecto "CollabApp".

---

## 🗣️ 1. ¿Qué es un Pull Request (PR) o Merge Request (MR)?

Un **Pull Request** (término usado en GitHub y Bitbucket) o **Merge Request** (término usado en GitLab) es una solicitud formal para fusionar (merge) los cambios de una rama (la "rama fuente" o "head branch") en otra rama (la "rama base" o "target branch", usualmente `main` o `develop`).

Pero es mucho más que solo una solicitud de fusión:

*   **Plataforma de Discusión:** Los PRs proporcionan un espacio para discutir los cambios propuestos. Los miembros del equipo pueden hacer preguntas, ofrecer sugerencias y debatir la implementación.
*   **Revisión de Código (Code Review):** Es el lugar donde se realiza la revisión formal del código. Los revisores pueden examinar los cambios línea por línea, dejar comentarios y solicitar modificaciones.
*   **Integración Continua (CI):** Muchos equipos integran herramientas de CI que ejecutan pruebas automatizadas en el código del PR antes de que se pueda fusionar.
*   **Historial y Trazabilidad:** Un PR cerrado (fusionado o no) deja un registro de la discusión y el proceso de decisión sobre un conjunto de cambios.

>   **En CollabApp:** Cuando Ana termina la funcionalidad `feature/crear-tarea`, no la fusiona directamente a `main`. En su lugar, abre un Pull Request para que Bruno y/o Carla revisen su trabajo.

---

## 🔄 2. El Flujo de un Pull Request (PR)

El ciclo de vida típico de un PR es el siguiente:

1.  **Desarrollo en una Rama:**
    *   Un desarrollador (ej. Ana) crea una nueva rama (ej. `feature/nueva-funcionalidad`) a partir de la rama base (`main`).
    *   Ana trabaja en esta rama, haciendo commits con sus cambios.
    *   Ana empuja (push) su rama a GitHub: `git push -u origin feature/nueva-funcionalidad`.

2.  **Apertura del Pull Request:**
    *   Ana va a la página del repositorio en GitHub.
    *   GitHub a menudo detecta automáticamente las ramas nuevas que se han empujado y ofrece crear un PR.
    *   Si no, Ana puede ir a la pestaña "Pull requests" y hacer clic en "New pull request".
    *   Selecciona la **rama base** (ej. `main`) y la **rama a comparar/fuente** (ej. `feature/nueva-funcionalidad`).
    *   Escribe un título claro y una descripción detallada para el PR.
    *   Asigna revisores (reviewers) y, si aplica, etiquetas (labels) o hitos (milestones).
    *   Hace clic en "Create pull request".

3.  **Discusión y Revisión de Código:**
    *   Los revisores asignados (ej. Bruno, Carla) reciben una notificación.
    *   Examinan los cambios en la pestaña "Files changed" del PR.
    *   Dejan comentarios, hacen preguntas, sugieren mejoras.
    *   El autor del PR (Ana) responde a los comentarios y puede hacer más commits en su rama `feature/nueva-funcionalidad` para abordar el feedback.
        *   **Importante:** Al empujar nuevos commits a la rama que ya tiene un PR abierto, el PR se actualiza automáticamente con esos nuevos cambios. No es necesario cerrar y abrir un nuevo PR.

4.  **Aprobación:**
    *   Una vez que los revisores están satisfechos con los cambios (y las pruebas automatizadas, si las hay, pasan), aprueban el PR.

5.  **Fusión (Merge):**
    *   Alguien con permisos (usualmente el autor del PR o un líder de equipo) fusiona el PR. Esto integra los cambios de `feature/nueva-funcionalidad` en `main`.
    *   GitHub ofrece diferentes estrategias de fusión (las veremos en el Módulo 5).

6.  **Cierre y Limpieza (Opcional pero Recomendado):**
    *   El PR se cierra automáticamente después de la fusión.
    *   La rama de funcionalidad (`feature/nueva-funcionalidad`) puede ser eliminada de GitHub (GitHub suele ofrecer un botón para esto) y también localmente.

---

## ✍️ 3. Creando un Pull Request en GitHub

*   *Caso CollabApp:* Ana ha terminado su trabajo inicial en la rama `feature/crear-tarea` y la ha empujado a GitHub. Ahora quiere proponer estos cambios para `main`.

    1.  **Ir a GitHub:** Ana navega al repositorio `CollabApp` en GitHub.
    2.  **Iniciar el PR:**
        *   A menudo, GitHub mostrará una notificación amarilla: "`feature/crear-tarea` had recent pushes less than a minute ago" con un botón "Compare & pull request". Ana hace clic ahí.
        *   Alternativamente, puede ir a la pestaña "Pull requests" y hacer clic en "New pull request".
    3.  **Seleccionar Ramas:**
        *   **`base:`** `main` (la rama a la que quiere fusionar)
        *   **`compare:`** `feature/crear-tarea` (la rama que contiene sus cambios)
        GitHub mostrará una vista previa de los cambios y si hay conflictos (¡esperemos que no!).
    4.  **Completar los Detalles del PR:**
        *   **Título:** Un título conciso y descriptivo.
            *   *Ejemplo para Ana:* `feat: Implementar funcionalidad básica de creación de tareas`
        *   **Descripción (Cuerpo):** Esta es la parte crucial. Debería explicar:
            *   **¿Qué hace este PR?** (Resumen de los cambios).
            *   **¿Por qué es necesario este cambio?** (Contexto, problema que resuelve, issue que cierra).
            *   **¿Cómo se probaron los cambios?** (Pasos para que los revisores puedan verificar).
            *   **(Opcional)** Capturas de pantalla, GIFs de la nueva UI.
            *   **(Opcional)** Si cierra un "Issue" de GitHub, puede escribir `Closes #ID_DEL_ISSUE` (ej. `Closes #12`). Esto vinculará el PR al issue y lo cerrará automáticamente cuando el PR se fusione.
            *   *Ejemplo de descripción para Ana:*
                ```markdown
                Este PR introduce la funcionalidad básica para que los usuarios puedan crear nuevas tareas en CollabApp.

                **Cambios Realizados:**
                - Añadido `task-form.html` con la estructura del formulario.
                - Creado `task-form.js` para manejar la entrada del usuario (sin lógica de guardado aún).
                - Actualizado `README.md` para mencionar esta nueva característica.

                **Motivación:**
                Este es el primer paso para permitir a los usuarios añadir contenido a la aplicación.
                Relacionado con el Issue #3 (Definir flujo de creación de tareas).

                **Cómo Probar:**
                1.  Navegar a `task-form.html` en el navegador.
                2.  Verificar que el formulario se muestra correctamente.
                3.  (No hay funcionalidad de guardado aún).

                @Bruno @Carla ¡Por favor, revisen!
                ```
        *   **Reviewers (Revisores):** En el panel derecho, Ana selecciona a Bruno y Carla como revisores.
        *   **Assignees (Asignados):** Ana puede asignarse a sí misma como responsable del PR.
        *   **Labels (Etiquetas):** Puede añadir etiquetas como `enhancement`, `frontend`, `needs-review`.
        *   **Projects/Milestones:** Si se usan, se pueden vincular aquí.
    5.  **Crear el PR:** Ana hace clic en "Create pull request".

    El PR ahora está abierto, y Bruno y Carla recibirán notificaciones para revisarlo.

---

## 🔄 4. El Ciclo de Vida de un PR: Discusión y Actualizaciones

Una vez que el PR está abierto:

1.  **Notificación a Revisores:** Bruno y Carla son notificados.
2.  **Revisión:** (Esto se detalla en el Módulo 4). Los revisores miran los archivos cambiados, dejan comentarios, etc.
3.  **Feedback y Cambios Adicionales:**
    *   Supongamos que Bruno encuentra un pequeño error o sugiere una mejora en el `task-form.js` de Ana.
    *   Ana ve el comentario de Bruno.
    *   Ana hace los cambios necesarios **en su rama local `feature/crear-tarea`**.
    *   Hace un nuevo commit: `git commit -m "fix: Corregir error en validación de formulario según feedback"`.
    *   Empuja (push) esos nuevos commits a la misma rama en GitHub: `git push origin feature/crear-tarea`.
    *   **¡Magia!** El Pull Request en GitHub se actualiza automáticamente para incluir estos nuevos commits. Bruno y Carla verán los cambios más recientes.
4.  **Repetir:** Este ciclo de revisión-feedback-cambio puede repetirse hasta que todos estén satisfechos.
5.  **Aprobación:** Los revisores marcan el PR como "Approved".
6.  **Fusión:** (Se detalla en el Módulo 5).

---

## 🛠️ Práctica Sugerida

???+ exercise "Ejercicio: Abriendo tu Primer Pull Request"
    **Escenario:** Continúas con el trabajo de la rama `feature/mostrar-lista-tareas` (o la que creaste en el Módulo 2) en el proyecto "CollabApp" (o tu proyecto de práctica).
    1.  **Asegurar Cambios en GitHub:**
        *   Si no lo hiciste al final del Módulo 2, asegúrate de que tu rama de funcionalidad (ej. `feature/mostrar-lista-tareas`) con sus commits esté empujada (push) a GitHub.
            ```bash
            # (Estando en tu rama de funcionalidad)
            git push origin feature/mostrar-lista-tareas 
            ```
            *(Si ya hiciste el `git push -u ...` antes, solo `git push` es suficiente).*

    2.  **Crear el Pull Request en GitHub:**
        *   Ve a la página de tu repositorio en GitHub.
        *   Busca la notificación para crear un PR para tu rama o ve a la pestaña "Pull requests" y haz clic en "New pull request".
        *   **Base:** Selecciona `main`.
        *   **Compare:** Selecciona tu rama de funcionalidad (ej. `feature/mostrar-lista-tareas`).
        *   **Título:** Escribe un título claro, ej: `feat: Implementar visualización inicial de la lista de tareas`.
        *   **Descripción:**
            *   Describe brevemente qué hace el PR.
            *   Menciona los archivos principales que modificaste.
            *   Si estás practicando solo, puedes escribir: "Este PR añade la estructura básica para mostrar la lista de tareas. Listo para revisión (por mí mismo en este caso de práctica 😉)."
            *   Si estás practicando con un compañero, menciónalo con `@nombredeusuario` y pídele que revise.
        *   **Reviewers:** Si tienes un compañero, asígnaselo. Si estás solo, puedes omitir esto o asignarte a ti mismo (aunque es un poco redundante).
        *   **Labels:** (Opcional) Añade una etiqueta como `feature` o `frontend`.
        *   Haz clic en "Create pull request".

    3.  **Explorar el PR Creado:**
        *   Una vez creado, explora las diferentes pestañas del PR:
            *   **Conversation:** Donde verás la descripción y donde aparecerán los comentarios.
            *   **Commits:** Lista de los commits incluidos en este PR.
            *   **Checks:** (Si hay CI configurada) Estado de las pruebas.
            *   **Files changed:** ¡La más importante para la revisión! Aquí ves las diferencias (diffs) de cada archivo modificado.

    4.  **(Opcional - Si tienes un compañero o quieres simularlo): Iterar**
        *   Imagina que un revisor te pide un pequeño cambio (ej. cambiar el texto de un título en `task-list.html`).
        *   En tu máquina local, en tu rama de funcionalidad (`feature/mostrar-lista-tareas`):
            *   Haz el cambio solicitado en `task-list.html`.
            *   `git add task-list.html`
            *   `git commit -m "style: Actualizar título según feedback de revisión"`
            *   `git push origin feature/mostrar-lista-tareas`
        *   Vuelve al PR en GitHub y observa cómo se actualiza automáticamente con el nuevo commit y los cambios en la pestaña "Files changed".

---

!!! success "✅ Puntos Clave del Módulo 3"
    *   Un **Pull Request (PR)** es el mecanismo para proponer y discutir la integración de cambios de una rama a otra (generalmente `main`).
    *   Flujo básico: `crear rama` ➡️ `hacer commits` ➡️ `push de la rama` ➡️ `abrir PR en GitHub`.
    *   Un buen PR tiene un **título claro** y una **descripción detallada**.
    *   Los PRs son el lugar para la **revisión de código** y la discusión.
    *   Los nuevos commits empujados a una rama con un PR abierto **actualizan automáticamente el PR**.

---

¡Excelente! Ahora que sabes cómo proponer cambios formalmente, el siguiente paso es aprender cómo realizar y recibir revisiones de código efectivas dentro de estos Pull Requests. ¡Nos vemos en el Módulo 4!