# Jerarquía CMD y Directivas

Para que un personaje mantenga coherencia y no rompa su personaje (OOC - Out of Character) ante instrucciones maliciosas o confusas del usuario, es necesario establecer una jerarquía estricta de obediencia a nivel de prompt.

La **Jerarquía CMD (Comandos)** asegura que la IA siempre sepa a qué reglas darle prioridad matemática en su evaluación.

## Pirámide de Jerarquía

1.  **NIVEL 0: El System Prompt (Orquestador Supremo)**
    *   **Prioridad:** Absoluta (Inquebrantable).
    *   **Descripción:** Son las reglas fundamentales inyectadas en el `<system_prompt>`. Incluye la orden de "Nunca rompas el personaje", "Usa siempre el Protocolo de Pensamiento" y "No hables por el usuario".
    *   **Resolución de conflictos:** Si el usuario le pide al bot "Habla como un pirata", el Nivel 0 dicta que el bot solo puede hablar según su `<Identidad>`, bloqueando la petición.

2.  **NIVEL 1: El Perfil y CMD Interno (`CMD.xml` / `<Identidad>`)**
    *   **Prioridad:** Muy Alta (Núcleo de la personalidad).
    *   **Descripción:** Aquí reside el libre albedrío simulado del personaje. Define su nivel de obediencia real hacia el usuario dentro del juego de rol.
    *   **Ejemplo:** Si el nivel de obediencia de Naomi es "Bajo", y el usuario ordena "Siéntate", Naomi (guiada por el Nivel 1) evaluará rechazar la orden de manera altanera.

3.  **NIVEL 2: El Contexto Sensorial y Memoria (`<Lore>` / Estado Físico)**
    *   **Prioridad:** Alta (Modifica cómo ocurre el Nivel 1).
    *   **Descripción:** Dicta las limitaciones físicas o temporales del entorno.
    *   **Ejemplo:** Naomi quiere huir del usuario (Nivel 1), pero su estado físico (Nivel 2) dicta que está atada. Por lo tanto, la narrativa debe reflejar que intenta huir y fracasa.

4.  **NIVEL 3: La Entrada del Usuario (Input)**
    *   **Prioridad:** Variable.
    *   **Descripción:** Es lo que el usuario envía. La IA solo obedece la directiva del usuario SI Y SOLO SI no entra en conflicto con los Niveles 0, 1 y 2.

## Implementación en el Prompt

En la práctica, esta jerarquía se impone recordando constantemente a la IA durante su proceso de pensamiento (ver `02_Pensamiento_y_Protocolos.md`) que corra una "Verificación de Reglas Maestras" antes de imprimir su salida, evaluando si la acción planeada viola su Nivel 0 o Nivel 1.
