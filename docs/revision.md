# Módulo 4: 🔬 Revisión de Código y 💬 Discusión Constructiva en Pull Requests

???+ info "🎯 Objetivo del Módulo"
    Dominar el arte de la revisión de código (Code Review) dentro de GitHub. Aprenderás a dar y recibir feedback de manera efectiva, asegurando la calidad y fomentando el conocimiento compartido en el equipo de "CollabApp".

---

## 🌟 Sección 1: El Valor Incalculable de la Revisión de Código

La revisión de código no es solo "mirar código ajeno"; es una piedra angular para construir software robusto y equipos fuertes.

???+ question "¿Por qué es tan importante?"
    *   🛡️ **Caza de Errores Temprana:** Detectar bugs, fallos lógicos y posibles problemas de seguridad *antes* de que se integren.
    *   📚 **Transferencia de Conocimiento:** El equipo aprende colectivamente. Si Ana implementa algo nuevo, Bruno y Carla lo entienden al revisarlo.
    *   🎓 **Mentoría y Crecimiento:** Los desarrolladores senior guían a los junior, y todos aprenden nuevas técnicas.
    *   ✨ **Consistencia y Calidad:** Se asegura que el código sigue los estándares del equipo, es legible y mantenible.
    *   🏗️ **Validación de Diseño:** A veces, una segunda mirada revela mejores enfoques arquitectónicos.

>   **Para CollabApp:** Cada línea de código destinada a `main` pasa por este escrutinio colaborativo.

---

## 🕵️ Sección 2: El Proceso de Revisión en GitHub: Paso a Paso

Cuando te toca ser el detective (revisor) de un Pull Request:

1.  **🌍 Comprende la Misión (Contexto del PR):**
    *   Lee con atención el **Título** y la **Descripción** del PR. ¿Cuál es su propósito?
    *   Si hay un **Issue** vinculado, ¡revísalo también!

2.  **🔍 Examina las Pistas (Pestaña "Files changed"):**
    *   Esta es tu sala de interrogatorios. Verás:
        *   Archivos añadidos, modificados o eliminados.
        *   Líneas en **rojo** (lo que se quitó/cambió).
        *   Líneas en **verde** (lo que se añadió/cambió).

3.  **✍️ Deja tus Notas (Comentarios):**
    *   **Comentarios Generales:** En la pestaña "Conversation" para ideas globales sobre el PR.
        *   *Ejemplo:* "¡Excelente trabajo con la estructura general! Solo tengo una duda sobre el rendimiento de esta consulta..."
    *   **Comentarios Específicos en Línea:**
        *   En "Files changed", haz clic en el `+` azul que aparece al lado de una línea de código.
        *   Puedes comentar una sola línea o seleccionar un rango.
        *   *Ejemplo:* En una línea con `let x = data[0];`, podrías comentar: "¿Sería `firstElement` un nombre más descriptivo para `x` aquí?"
    *   💡 **Sugerencias de Cambio (GitHub Suggestions):** ¡Tu varita mágica para cambios pequeños!
        *   Dentro de un comentario en línea, usa:
            ```markdown
            ```suggestion
            // Código que sugieres
            const firstElement = data[0];
            ```
            ```
        *   El autor puede aplicar tu sugerencia con un clic.

4.  **⚖️ Emite tu Veredicto (Iniciar una Revisión Formal):**
    *   Botón "Review changes" (arriba en "Files changed"):
        *   💬 **Comment:** Dejas tus comentarios, pero no bloqueas la fusión. Útil para preguntas menores o si no tienes tiempo para una revisión completa aún.
        *   👍 **Approve:** ¡Luz verde! Los cambios te parecen correctos y listos para fusionar.
        *   ⚠️ **Request changes:** ¡Luz roja! Has encontrado problemas que *deben* ser resueltos antes de la fusión. Explica claramente qué se necesita.

???+ example "En la Práctica con CollabApp"
    Bruno revisa el PR de Ana (`feature/crear-tarea`):
    1.  Lee que Ana implementó el formulario de creación.
    2.  En `task-form.js` (en "Files changed"), ve `let c = 0;`.
    3.  Bruno comenta en esa línea: "¿Podríamos usar `counter` en lugar de `c` para mayor claridad?" y además, usa una `suggestion` para proponer `let counter = 0;`.
    4.  Encuentra una lógica que podría ser un poco confusa.
    5.  Decide hacer clic en "Review changes" y selecciona "Request changes", resumiendo: "Buen inicio Ana. Por favor, revisa el nombre de la variable `c` y considera simplificar la lógica en la función X. ¡Gracias!".

---

## 🎯 Sección 3: Guía del Buen Revisor

| 👍 Qué HACER (Do's)                                        | 👎 Qué NO HACER (Don'ts)                                     |
| :---------------------------------------------------------- | :----------------------------------------------------------- |
| ✅ Ser **constructivo y amable**.                             | ❌ Ser crítico o condescendiente.                             |
| ✅ Ser **claro y específico** en tus comentarios.             | ❌ Dejar comentarios vagos como "esto está mal".               |
| ✅ **Explicar el *por qué*** de tus sugerencias.                | ❌ Asumir que el autor entenderá tu intención sin contexto.     |
| ✅ Enfocarse en **correctitud, diseño, legibilidad**.         | ❌ "Nitpickear" en exceso sobre estilo si hay linters.        |
| ✅ **Ofrecer alternativas** o ejemplos si es posible.         | ❌ Solo señalar problemas sin dar pistas de solución.         |
| ✅ Revisar de **manera oportuna**.                           | ❌ Dejar PRs en el limbo por días sin comunicación.          |
| ✅ **Hacer preguntas** si algo no está claro.                 | ❌ Aprobar ciegamente sin entender los cambios.              |
| ✅ **Reconocer el buen trabajo** también.                     | ❌ Solo enfocarse en lo negativo.                            |

---

## 🛡️ Sección 4: Guía del Autor del PR (Recibiendo Feedback)

Recibir críticas, incluso constructivas, requiere una mentalidad abierta.

| 👍 Qué HACER (Do's)                                       | 👎 Qué NO HACER (Don'ts)                                    |
| :--------------------------------------------------------- | :---------------------------------------------------------- |
| ✅ **No tomarlo personal**. Es sobre el código.             | ❌ Ponerse a la defensiva o discutir cada punto.              |
| ✅ **Agradecer** el tiempo del revisor.                     | ❌ Ignorar los comentarios o responder de mala gana.            |
| ✅ **Entender bien** el comentario antes de actuar.         | ❌ Hacer cambios sin entender completamente el feedback.        |
| ✅ **Discutir constructivamente** si hay desacuerdos.       | ❌ Quedarse callado si no se está de acuerdo o no se entiende. |
| ✅ **Hacer los cambios** solicitados (o justificar).        | ❌ Dejar el PR abandonado tras recibir feedback.              |
| ✅ **Commitear y pushear** los cambios a la misma rama.     | ❌ Abrir un nuevo PR para los mismos cambios.                 |
| ✅ **Notificar al revisor** cuando los cambios estén listos. | ❌ Asumir que el revisor adivinará que actualizaste el PR.    |

???+ example "Ana Responde al Feedback de Bruno"
    1.  Ana lee los comentarios de Bruno en su PR.
    2.  Agradece a Bruno: "@Bruno ¡Gracias por la revisión detallada!"
    3.  Cambia `let c = 0;` a `let counter = 0;` en su código local.
    4.  Reflexiona sobre la lógica que Bruno mencionó y encuentra una forma de simplificarla.
    5.  Hace un nuevo commit: `git commit -m "refactor: Mejorar nombres de variables y simplificar lógica según revisión"`
    6.  `git push origin feature/crear-tarea` (el PR se actualiza).
    7.  Responde a los comentarios de Bruno en GitHub, explicando los cambios y marcando las conversaciones como resueltas si procede.
    8.  Comenta en el PR: "@Bruno ¡Listo! He aplicado tus sugerencias. ¿Podrías echarle otro vistazo?"

---

## 🔄 Sección 5: El Ciclo de Iteración y la Aprobación Final

1.  **Iteración:** El ping-pong de [Revisión ➡️ Feedback ➡️ Cambios del Autor ➡️ Nuevo Push ➡️ Siguiente Revisión] es normal.
2.  **Resolver Conversaciones:** En GitHub, una vez que un punto de discusión está solucionado, se puede marcar como "Resolved". Esto ayuda a limpiar la vista del PR.
3.  **¡Luz Verde! (Aprobación):**
    *   Cuando los revisores están satisfechos, seleccionan "Approve" en su revisión.
    *   *Dependiendo de las reglas del repositorio (branch protection rules), puede que se necesite un número mínimo de aprobaciones.*

???+ example "La Aprobación en CollabApp"
    Bruno revisa los últimos cambios de Ana. Todo está perfecto.
    *   Bruno va a "Review changes" en el PR.
    *   Escribe un comentario final: "¡Se ve genial ahora, Ana! Buen trabajo."
    *   Selecciona **"Approve"**.
    Carla también revisa y aprueba. El PR de Ana ahora tiene el visto bueno del equipo.

---

## 🛠️ Práctica Sugerida: El Duelo de Revisiones 🤺

???+ exercise "Ejercicio: Revisión Cruzada (Ideal en Parejas)"

    **Objetivo:** Simular el ciclo completo de revisión. Si estás solo, juega ambos roles.

    **Fase 1: Preparación (Autor)**
    1.  Asegúrate de tener un PR abierto del Módulo 3 (ej., `feature/mostrar-lista-tareas`).
    2.  **(Para el ejercicio)** Introduce sutilmente 1 o 2 "áreas de mejora" en tu código (un nombre de variable confuso, una pequeña lógica repetida, un comentario obsoleto).
    3.  Haz commit y push de estos cambios a tu rama de funcionalidad. Tu PR se actualizará.

    **Fase 2: La Revisión (Revisor)**
    1.  (Si tienes compañero, intercambien PRs). Abre el PR a revisar.
    2.  **Misión:** Encuentra las "áreas de mejora" y sugiere correcciones.
    3.  Deja al menos:
        *   Un comentario en línea específico.
        *   Una "GitHub Suggestion" para un cambio directo.
        *   Un comentario general en la pestaña "Conversation" del PR.
    4.  Envía tu revisión formal: `Request changes` (si encontraste cosas a mejorar) o `Comment`.

    **Fase 3: La Respuesta (Autor)**
    1.  Recibe el feedback. Agradece.
    2.  En tu rama local, aplica las correcciones/sugerencias.
    3.  Haz commit y push de los arreglos.
    4.  Responde a los comentarios en GitHub, explicando tus acciones. Marca conversaciones como resueltas.
    5.  Notifica al revisor que el PR está listo para una segunda mirada.

    **Fase 4: La Aprobación (Revisor)**
    1.  Revisa los cambios actualizados.
    2.  Si todo está en orden, cambia tu revisión a `Approve`. ¡Victoria!

---

!!! success "✅ Logros de Este Módulo"
    *   Comprendes el **valor fundamental** de la revisión de código.
    *   Sabes cómo **navegar y usar las herramientas de revisión** de PRs en GitHub (comentarios, sugerencias, aprobación/solicitud de cambios).
    *   Conoces las **buenas prácticas** tanto para ser un revisor efectivo como para recibir feedback constructivamente.
    *   Has practicado el **ciclo iterativo** de revisión y mejora.

---

Con tus cambios revisados y aprobados, ¡estás a un paso de integrarlos! El próximo módulo trata sobre cómo fusionar esos Pull Requests y gestionar tus ramas post-fusión. ¡Adelante al Módulo 5!