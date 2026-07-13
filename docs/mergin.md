# **Módulo 5: 🧬 Fusión (Merging) de Cambios**

???+ info "🎯 Objetivo del Módulo"
    Aprender a integrar (fusionar) los Pull Requests aprobados en la rama principal (`main`). Entender las diferentes estrategias de fusión que ofrece GitHub y cómo mantener el repositorio limpio eliminando ramas que ya no son necesarias. ¡Es hora de que el trabajo de Ana para "CollabApp" vea la luz en `main`!

---

##  **Sección 1: Fusionando un Pull Request Aprobado**

Una vez que un Pull Request (PR) ha sido revisado, discutido y **aprobado** por el equipo (y todas las comprobaciones automatizadas, si las hay, han pasado), está listo para ser fusionado.

???+ check "Requisitos Previos para la Fusión (Generalmente)"
    *   ✅ Al menos una aprobación (o el número requerido por las reglas de protección de rama).
    *   ✅ No hay solicitudes de cambio pendientes ("Request changes").
    *   ✅ No hay conflictos de fusión con la rama base (GitHub lo indicará).
    *   ✅ (Idealmente) Las pruebas automatizadas (CI) pasan con éxito.

**¿Quién fusiona?** Usualmente, puede ser:
*   El autor del PR (Ana, en nuestro caso de CollabApp).
*   Un líder de equipo o alguien con permisos de merge en el repositorio.

**El Botón Mágico: "Merge pull request"**
En la página del PR en GitHub, una vez que se cumplen las condiciones, aparecerá un botón verde grande: **"Merge pull request"**.

*   *Caso CollabApp:* El PR de Ana para `feature/crear-tarea` ha sido aprobado por Bruno y Carla. Ana ve el botón "Merge pull request" activo.

---

## **Sección 2: Estrategias de Fusión en GitHub**

Al hacer clic en la flecha desplegable junto al botón "Merge pull request", GitHub ofrece varias estrategias. Las tres principales son:

???+ details "Estrategias de Fusión Detalladas"
   

    ???+ tip "1. Create a merge commit (Crear un commit de fusión) - Opción por defecto"
        *   **Cómo funciona:** Todos los commits de la rama de funcionalidad (ej. `feature/crear-tarea`) se añaden al historial de `main`. Además, se crea un **commit de fusión** especial en `main` que une las dos historias (la de `main` y la de `feature/crear-tarea`).
        *   **Resultado en el historial:** Mantiene todo el historial detallado de la rama de funcionalidad. El historial de `main` se verá como dos líneas que se unen.
        *   **Ventajas:**
            *   Preserva todo el contexto y el historial granular de la rama.
            *   Es fácil revertir toda la funcionalidad si es necesario (revirtiendo el commit de fusión).
            *   Claro para ver cuándo se integró una rama de funcionalidad.
        *   **Desventajas:** Puede hacer que el historial de `main` se vea un poco "ruidoso" con muchos commits de          fusión si hay muchas ramas pequeñas.
        
         👍**Recomendado para la mayoría de los equipos, especialmente al empezar.**

    ???+ tip "2. Squash and merge (Comprimir y fusionar)"
        *   **Cómo funciona:** Combina todos los commits de la rama de funcionalidad en **un solo commit** en la rama `main`. GitHub te permite editar el mensaje de este único commit, generalmente tomando los mensajes de los commits originales como cuerpo.
        *   **Resultado en el historial:** El historial de `main` se mantiene lineal y limpio, con un solo commit representando toda la funcionalidad. No se crea un commit de fusión explícito.
        *   **Ventajas:**
            *   Historial de `main` muy limpio y fácil de leer.
            *   Cada commit en `main` representa una funcionalidad completa o un arreglo.
        *   **Desventajas:**
            *   Se pierde el historial detallado de los commits intermedios de la rama de funcionalidad (aunque siguen existiendo en la rama original si no se borra).
            *   Más difícil revertir solo una parte de los cambios de la rama original.
        
        👍 **Bueno para equipos que prefieren un historial de `main` muy lineal y conciso.**

    ???+ tip "3. Rebase and merge (Reorganizar y fusionar)"
        

        *   **Cómo funciona:** Toma todos los commits de la rama de funcionalidad y los "reaplica" uno por uno encima del último estado de la rama `main`. No se crea un commit de fusión.
        *   **Resultado en el historial:** El historial de `main` se mantiene perfectamente lineal, como si todos los commits de la rama de funcionalidad se hubieran hecho directamente en `main`.
        *   **Ventajas:**
            *   El historial más limpio y lineal posible.
        *   **Desventajas:**
            *   **Puede ser peligroso si la rama ha sido compartida y otros han basado trabajo en ella, ya que reescribe el historial de la rama.**
            *   Se pierde la información contextual de que esos commits provenían de una rama de funcionalidad específica (a menos que se indique en los mensajes de commit).
            *   Puede ser más complejo de manejar si hay conflictos durante el rebase.
        
        ⚠️ **Usar con precaución y entendimiento. Generalmente para usuarios más avanzados o flujos de trabajo específicos.**

*   **Caso CollabApp:** Ana decide usar la opción por defecto: **"Create a merge commit"** para su PR `feature/crear-tarea`.
    1.  Hace clic en "Merge pull request".
    2.  GitHub le pide confirmar el mensaje del commit de fusión (generalmente lo autocompleta bien).
    3.  Hace clic en "Confirm merge".
    ¡Listo! Los cambios de `feature/crear-tarea` ahora están en `main`.

---

## **Sección 3: Limpieza Post-Fusión: Eliminando Ramas**

Una vez que una rama de funcionalidad ha sido fusionada a `main` (y ya no se necesita para más desarrollo o correcciones sobre ese mismo PR), es una buena práctica eliminarla para mantener el repositorio ordenado.

???+ question "¿Cómo eliminar las ramas?"
    <summary>Pasos para Eliminar Ramas Post-Fusión</summary>

    1.  **Eliminar la Rama Remota (en GitHub):**
        *   Después de fusionar un PR, GitHub usualmente muestra un botón **"Delete branch"** en la página del PR. ¡Simplemente haz clic en él!
        *   Si no, puedes ir a la lista de ramas de tu repositorio en GitHub y eliminarla desde allí.

        *   *Caso CollabApp:* Después de fusionar, Ana ve el botón "Delete branch" para `feature/crear-tarea` y lo presiona. La rama ya no existe en GitHub.

    2.  **Eliminar la Rama Local:**
        La rama todavía existe en tu repositorio local. Para eliminarla:

        ```bash
        # Primero, asegúrate de no estar en la rama que quieres borrar.
        # Cambia a main y actualízala (muy importante después de un merge en el remoto):
        git checkout main
        git pull origin main  # Esto trae el commit de fusión (y otros cambios) a tu main local

        # Ahora, elimina la rama localmente:
        git branch -d nombre-de-la-rama-fusionada
        # Ejemplo: git branch -d feature/crear-tarea
        ```
        *   `-d` (minúscula) es seguro: solo borrará la rama si ya ha sido fusionada a la rama actual (`main` en este caso) o a otra rama que tenga `main` como ancestro.
        *   `-D` (MAYÚSCULA) fuerza la eliminación, incluso si la rama no ha sido fusionada. **¡Úsalo con mucho cuidado!**

???+ warning "¡Actualiza `main` Local Primero!"
    Es crucial hacer `git checkout main` y luego `git pull origin main` **antes** de intentar borrar la rama local con `-d`. Si no, tu Git local no sabrá que la rama ya fue fusionada en el remoto, y `git branch -d` podría dar un error diciendo que la rama no está completamente fusionada.

---

## **Sección 4: Manteniendo tu `main` Local Actualizado**

Después de que un PR es fusionado a `main` en GitHub (ya sea por ti o por un compañero), tu copia local de `main` se queda "atrás". Debes actualizarla para tener los últimos cambios.

**Flujo recomendado:**

    ```bash
    # 1. Cambia a tu rama main local
    git checkout main

    # 2. Trae los cambios de la rama main remota (de GitHub) y fusiónalos
    git pull origin main
    
    ```
 Haz esto regularmente, especialmente antes de crear nuevas ramas de funcionalidad, para asegurarte de que partes del código más reciente.
 
 **Caso CollabApp:** Bruno y Carla, después de ver que el PR de Ana fue fusionado, ejecutan en sus máquinas:
    ```bash
    git checkout main
    git pull origin main
    
    ```
Ahora sus ramas main locales tienen la funcionalidad de "creación de tareas".

🛠️ **Práctica Sugerida**
???+ exercise "Ejercicio: Fusión y Limpieza"
    **Escenario:** Usarás el PR que aprobaste (o te aprobaron) en el Módulo 4.

    1.  **Fusionar el Pull Request:**
        *   Ve al PR aprobado en GitHub.
        *   Revisa las opciones de fusión (puedes experimentar con "Squash and merge" si te sientes aventurero y el PR es tuyo, pero "Create a merge commit" es lo más seguro para empezar).
        *   Haz clic en "Merge pull request" y luego en "Confirm merge".
        *   ¡Observa cómo el PR cambia su estado a "Merged"!

    2.  **Eliminar la Rama Remota:**
        *   En la página del PR recién fusionado, busca y haz clic en el botón "Delete branch".
        *   Verifica en la lista de ramas de tu repositorio en GitHub que la rama de funcionalidad ya no está.

    3.  **Actualizar `main` Local y Eliminar Rama Local:**
        *   En tu terminal, en tu repositorio local:
            ```bash
            git checkout main
            git pull origin main
            ```
        *   Verifica el historial con `git log --oneline --graph`. Deberías ver el commit de fusión (o el commit "squashed").
        *   Ahora, elimina la rama de funcionalidad localmente:
            ```bash
            git branch -d nombre-de-tu-rama-funcionalidad
            # Ejemplo: git branch -d feature/mostrar-lista-tareas
            ```
        *   Verifica con `git branch` que la rama local ha sido eliminada.

    4.  **(Si trabajas con un compañero): Sincronización del Compañero**
        *   El compañero que NO fusionó el PR debe ahora actualizar su `main` local:
            ```bash
            git checkout main
            git pull origin main
            ```
        *   También debería eliminar su copia local de la rama de funcionalidad (si la tenía y ya no la necesita):
            ```bash
            git branch -d nombre-de-la-rama-funcionalidad-del-compañero
            ```

!!! success "✅ Logros de Este Módulo"
    * Sabes cómo fusionar un Pull Request aprobado en GitHub.
    * Comprendes las diferencias básicas entre las estrategias de fusión: "Create a merge commit", "Squash and merge", y "Rebase and merge".
    * Has aprendido la importancia de eliminar ramas fusionadas (tanto remotas como locales) para mantener el repositorio limpio.
    * Entiendes la necesidad de actualizar tu rama main local (git pull) después de las fusiones en el remoto.
    ¡Excelente trabajo! Has completado una parte fundamental del ciclo de desarrollo colaborativo. El siguiente desafío es aprender a manejar situaciones donde los cambios chocan: los temidos (pero manejables) conflictos de fusión. ¡Vamos al Módulo 6!
    **Cambios Realizados:**

    1.  **Sección 2 (Estrategias de Fusión):** He anidado las tres estrategias dentro de un desplegable principal llamado "Estrategias de Fusión Detalladas". Cada estrategia individual también tiene su propio `<summary>` para que, si el renderizador lo soporta, puedan ser desplegables anidados. Si no, al menos estarán agrupadas bajo el desplegable principal.
    2.  **Sección 3 (Eliminación de Ramas):** Los dos pasos (eliminar rama remota y local) ahora están dentro de un desplegable llamado "Pasos para Eliminar Ramas Post-Fusión".
    3.  **Práctica Sugerida:** Los cuatro pasos del ejercicio ahora están dentro de un desplegable llamado "Pasos del Ejercicio Práctico".

    
Verifica si esta estructura y la funcionalidad de los desplegables (si tu visor los soporta) son lo que esperabas. ¡Listo para el Módulo 6!

