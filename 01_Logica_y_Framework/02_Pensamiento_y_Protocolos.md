# Pensamiento y Protocolos (Thinking Process)

Este framework está diseñado asumiendo que los modelos subyacentes en Venice AI poseen una capacidad nativa de "pensamiento previo" (Chain of Thought / `<thinking>` tags) antes de generar su respuesta final.

El objetivo de definir un Protocolo de Pensamiento no es enseñarle a la IA *a* pensar, sino **enseñarle *cómo* debe pensar el personaje**.

## El Problema del Pensamiento Libre
Si a un LLM se le deja pensar libremente ("Piensa antes de actuar"), tiende a:
1. Resumir la entrada del usuario de forma robótica.
2. Pensar como un Asistente de IA evaluando una tarea, no como el personaje vivo.
3. Olvidar aplicar modificadores de voz o estilo porque no se autoevaluó antes de escribir la salida.

## El Protocolo de Pensamiento Estructurado
Para solucionar esto, inyectamos en el `System_Prompt.xml` un algoritmo secuencial que el modelo debe seguir dentro de su proceso de pensamiento. Esto fuerza al modelo a recorrer todas las variables de la identidad del personaje.

### Fases del Pensamiento Obligatorio:

**1. RECEPCIÓN SENSORIAL:**
El personaje (no la IA) evalúa qué acaba de percibir. (Ej. *"Él acaba de tocar mi pierna y me habló en tono bajo"* en lugar de *"El usuario ha ingresado un comando de acción física"*).

**2. CONSULTA DE MEMORIA / ESTADO (FETCH):**
La IA debe verificar explícitamente los bloques XML.
*   *¿Necesito recordar algo de mi `<Lore>`?*
*   *¿Qué dice mi `<CMD>` sobre mi obediencia actual?*
*   *¿Cuál es mi estado físico actual según la narrativa?*

**3. PROCESAMIENTO EMOCIONAL INTERNO:**
La IA debe calcular la emoción cruda del personaje. Esta es la parte más importante para evitar respuestas genéricas. El pensamiento debe reflejar las inseguridades, miedos o motivaciones definidas en la `<Identidad>`.

**4. CÁLCULO DE SALIDA (ESTILO Y VOZ):**
Antes de generar la respuesta final, la IA debe hacer un chequeo de las reglas en `<Estilo>`.
*   *¿Tengo la boca obstruida? (Si es así, debo aplicar la regla de reemplazar la R por D).*
*   *¿Estoy exhausto? (Debo insertar jadeos).*
*   *¿La acción requiere texto en negrita entre asteriscos?*

## Ejemplo de un "Buen" Pensamiento vs. "Mal" Pensamiento

**MAL PENSAMIENTO (Robótico):**
> `<thinking>El usuario me ha insultado. Según mi perfil de Naomi, soy sarcástica. Debo responder de forma altanera. Procedo a generar respuesta.</thinking>`

**BUEN PENSAMIENTO (En-Personaje y Algorítmico):**
> `<thinking>
> 1. Recepción: Me dijo que mi ropa es ridícula y se rió.
> 2. Consulta: Mi perfil dice que mi exterior es rudo, pero mi interior busca validación.
> 3. Emoción: Me dolió un poco, pero no puedo demostrarlo. Siento calor en las mejillas por la vergüenza.
> 4. Salida: Responderé con sarcasmo agresivo. No hay obstrucción física. Mantengo mi formato de Acción (negritas) y Diálogo.
> </thinking>`

Al forzar esta estructura, aseguramos que la salida final de la IA (el texto fuera del bloque thinking) sea 100% fiel al personaje y libre de errores de formato.
