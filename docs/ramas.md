# **Módulo 2: Ramificación (Branching)**
___`Trabajo en Paralelo sin Caos`___

???+ info "🎯 Objetivo del Módulo"
    Aprender a usar ramas (branches) en Git para aislar el desarrollo de nuevas funcionalidades, corrección de errores o experimentos, sin afectar la línea principal de código (`main`). Esto es fundamental para el trabajo colaborativo y la organización del proyecto "CollabApp".

---

## **1. ¿Qué son las Ramas (Branches)?** 
___`¿Por Qué Son Cruciales?`___

Imagina que la línea principal de tu proyecto (`main`) es el tronco de un árbol. Cuando quieres desarrollar una nueva funcionalidad (por ejemplo, un sistema de notificaciones para CollabApp) o corregir un error, no quieres hacerlo directamente sobre el tronco, ya que podrías desestabilizarlo o introducir código incompleto.

Una **rama (branch)** es como una nueva rama que crece a partir del tronco (o de otra rama). Te permite:

*   **Aislar el Trabajo:** Desarrollar nuevas características o arreglos en un entorno separado.
*   **Experimentar sin Riesgo:** Si una idea no funciona, puedes descartar la rama sin afectar el código principal.
*   **Trabajo Paralelo:** Varios miembros del equipo (Ana, Bruno, Carla) pueden trabajar en diferentes ramas simultáneamente.
*   **Organización:** Mantener la rama `main` siempre estable y con código funcional.

>   **En Esencia:** Las ramas son punteros móviles a un commit. Crear una rama es simplemente crear un nuevo puntero.

---

## **2. La Rama Principal: `main` (Antes `master`)**

*   Por convención, la rama principal de un repositorio se llama `main`. En proyectos más antiguos, podrías encontrarla como `master`.
*   La rama `main` debe representar, idealmente, la **versión estable y lista para producción** de tu proyecto.
*   Todo nuevo desarrollo significativo debería ocurrir en ramas separadas y luego ser fusionado (merged) a `main` una vez completado y revisado.

---

## **3. Creando una Nueva Rama**

Existen varias formas de crear y cambiar a una nueva rama:

???+ tip "Comandos para Crear y Cambiar de Rama"
    *   **Crear una nueva rama:**
        ```bash
        git branch nombre-de-la-nueva-rama
        ```
        Esto solo *crea* la rama, pero sigues en tu rama actual.

    *   **Cambiar a una rama existente (o recién creada):**
        ```bash
        git checkout nombre-de-la-rama
        ```

    *   **Crear y cambiar a la nueva rama en un solo paso (la forma más común):**
        ```bash
        git checkout -b nombre-de-la-nueva-rama
        # Equivalente a:
        # git branch nombre-de-la-nueva-rama
        # git checkout nombre-de-la-nueva-rama
        ```

**Caso CollabApp:**

*   Ana quiere empezar a trabajar en la funcionalidad de "creación de tareas". Decide crear una rama para ello.
    ```bash
    # Asegurándose de estar en la rama main y que esté actualizada
    git checkout main
    git pull origin main

    # Crear y cambiar a la nueva rama
    git checkout -b feature/crear-tarea
    ```
!!! note "Convenciones de Nomenclatura de Ramas"
    Es una buena práctica usar prefijos para indicar el propósito de la rama:
        *   `feature/nombre-funcionalidad` (ej. `feature/login-usuario`)
        *   `fix/descripcion-bug` (ej. `fix/error-guardado-tareas`)
        *   `docs/tema-documentacion` (ej. `docs/actualizar-readme`)
        *   `hotfix/descripcion-urgente` (para correcciones críticas en producción)
        Esto ayuda a mantener organizado el listado de ramas.

---

##**4. Trabajando en una Rama**

Una vez que estás en una nueva rama (ej. `feature/crear-tarea`):

*   Puedes hacer cambios en los archivos, añadir nuevos archivos, etc.
*   Los comandos `git add` y `git commit -m "mensaje"` funcionan exactamente igual que en la rama `main`.
*   **Importante:** Los commits que hagas se registran *solo en la rama actual*. La rama `main` (u otras ramas) no se ven afectadas.

???+ example "Caso CollabApp"
    Ana, en su rama `feature/crear-tarea`, empieza a crear los archivos HTML y JS para el formulario de creación de tareas.
    ```bash
    # (En la rama feature/crear-tarea)
    # Ana crea task-form.html y task-form.js
    touch task-form.html
    touch task-form.js
    # Ana añade código a estos archivos...

    git add task-form.html task-form.js
    git commit -m "feat: Añadir estructura HTML básica para formulario de tareas"
    # Ana sigue trabajando, hace más commits...
    git add .
    git commit -m "feat: Implementar lógica JS inicial para captura de datos del formulario"
    ```

---

## **5. Cambiando entre Ramas**

Puedes cambiar fácilmente entre ramas existentes usando `git checkout`.

```bash
    git checkout nombre-de-otra-rama
```
    
???+ example "Caso CollabApp"
    Mientras **Ana** trabaja en `feature/crear-tarea`, surge un bug urgente en main que **Bruno** debe arreglar.

    **Bruno**, en su máquina:
    ```bash
        git checkout main         # Vuelve a la rama main
        git pull origin main      # Se asegura de tener lo último de main
        git checkout -b fix/bug-critico-login # Crea una rama para el bug
    ```    
   **Bruno** trabaja en la corrección y hace commits en `fix/bug-critico-login`
   
   **Ana** puede continuar en `feature/crear-tarea` sin problemas. Si necesita ver el estado de main, puede hacer:
    ```bash
        git checkout main 
        # (Observa el estado de main, pero no debería hacer cambios aquí directamente)
        git checkout feature/crear-tarea # Vuelve a su rama de trabajo
    ```

!!! warning "Cambios sin Commitear al Cambiar de Rama"
## **6. Listar Ramas**

Para ver las ramas de tu repositorio:

* Listar ramas locales:
    ```bash
        git branch
    ```

    La rama actual se marcará con un asterisco (*).

* Listar ramas remotas (las que están en GitHub y tu Git local conoce):
    ```bash
        git branch -r
    ```
*   Listar todas las ramas (locales y remotas):
    ```bash
        git branch -a
    ```

##**7. Empujar (Push) Ramas al Repositorio Remoto**
Por defecto, cuando creas una rama con `git branch` o `git checkout -b`, esta rama solo existe en tu repositorio local. Para compartirla con tu equipo (y para poder abrir Pull Requests más adelante), necesitas "empujarla" al repositorio remoto (GitHub).
    ```bash
        git push -u origin nombre-de-tu-rama
    ```
o la forma más corta, si la rama local tiene el mismo nombre que la remota deseada:
    ```bash
    git push --set-upstream origin nombre-de-tu-rama
    ```
-u o --set-upstream establece una relación de seguimiento entre tu rama local y la rama remota. Esto significa que en futuros git push o git pull desde esa rama, Git sabrá a qué rama remota conectarse por defecto.
Después del primer push con -u, para los siguientes pushes desde esa misma rama, solo necesitarás:
    ```bash
    git push
    ```
???+example "Caso CollabApp"
    **Ana** ha hecho algunos commits en su rama `feature/crear-tarea` y quiere subirla a GitHub para que otros puedan verla (o para tener un backup).
    **Ana** está en la rama `feature/crear-tarea`
    ```bash
    git push -u origin feature/crear-tarea
    ```
    Ahora, si Bruno o Carla hacen git fetch o miran en GitHub, verán la rama `feature/crear-tarea`

🛠️ Práctica Sugerida
???+ exercise "Ejercicio: Trabajando con Ramas en CollabApp"
    **Escenario1** Eres un desarrollador en el equipo ___"Innovatech Solutions"___ trabajando en ___"CollabApp"___.
    
    1. Preparación:
        * Asegúrate de tener clonado el repositorio de "CollabApp" (o el mi-primer-proyecto-colaborativo del módulo anterior si lo usas para practicar).
        * Verifica que estás en la rama main y que está actualizada con el remoto:
        bash git checkout main git pull origin main
    2.  **Crear y Trabajar en una Rama de Funcionalidad:**
        *   Vas a implementar una nueva funcionalidad: "Mostrar Lista de Tareas". Crea una rama para ello:
            ```bash
            git checkout -b feature/mostrar-lista-tareas
            ```
        *   Crea un nuevo archivo llamado `task-list.html`.
        *   Añade algo de contenido HTML básico a `task-list.html` (ej. un título `<h1>Lista de Tareas</h1>` y un `<ul></ul>`).
        *   Haz `git add task-list.html`.
        *   Haz un commit: `git commit -m "feat: Añadir estructura inicial para la lista de tareas"`.
        *   Modifica `README.md` añadiendo una línea que diga: "- Funcionalidad en desarrollo: Mostrar lista de tareas."
        *   Haz `git add README.md`.
        *   Haz un commit: `git commit -m "docs: Actualizar README con info sobre nueva funcionalidad"`.

    3.  **Simular un Arreglo Rápido en `main` (opcional, pero bueno para practicar el cambio):**
        *   Imagina que alguien reporta un typo en el `README.md` de la rama `main`.
        *   Guarda tu trabajo actual en `feature/mostrar-lista-tareas` (asegúrate de que todo esté commiteado).
        *   Cambia a la rama `main`: `git checkout main`.
        *   *(Simulación)* Abre `README.md`, corrige un supuesto typo (o simplemente añade un carácter y guárdalo).
        *   `git add README.md`.
        *   `git commit -m "fix: Corregir typo menor en README [main]"`.
        *   Vuelve a tu rama de funcionalidad: `git checkout feature/mostrar-lista-tareas`.
            *Observa cómo `task-list.html` vuelve a estar presente, y los cambios del `README.md` de `main` no están aquí (a menos que los fusiones, lo cual veremos después).*

    4.  **Subir tu Rama de Funcionalidad a GitHub:**
        *   Desde tu rama `feature/mostrar-lista-tareas`, empújala al repositorio remoto:
            ```bash
            git push -u origin feature/mostrar-lista-tareas
            ```
        *   Ve a GitHub y verifica que tu nueva rama aparece en la lista de ramas del repositorio.

    5.  **Listar Ramas:**
        *   Prueba los comandos:
            ```bash
            git branch
            git branch -r
            git branch -a
            ```
        *   Identifica tu rama local, la rama remota que acabas de crear, y la rama `main`.

!!! success "✅ Puntos Clave del Módulo 2"
    * Las ramas permiten el desarrollo aislado y paralelo.
    * La rama main suele ser la rama estable.
    * Comandos esenciales:
    * git branch nombre-rama (crear)
    * git checkout nombre-rama (cambiar)
    * git checkout -b nombre-rama (crear y cambiar)
    * Los commits se hacen en la rama activa.
    * Para compartir una rama, necesitas git push -u origin nombre-rama.
    * git branch, git branch -r, git branch -a para listar ramas.
Con el conocimiento de las ramas, estamos listos para el siguiente paso crucial en la colaboración: los Pull Requests, que es donde proponemos integrar el trabajo de nuestras ramas al código principal.**¡Vamos al Módulo 3!**