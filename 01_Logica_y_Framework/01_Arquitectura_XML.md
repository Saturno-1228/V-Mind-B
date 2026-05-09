# Arquitectura XML del Framework para Venice AI

Este repositorio funciona como un entorno de trabajo estructurado para la creación y gestión de "System Prompts" y perfiles de personajes para Inteligencia Artificial. La arquitectura se basa en el uso de etiquetas XML para separar y clasificar la información, lo cual optimiza la retención de contexto y el procesamiento de atención de los LLMs.

## Por qué XML
Los Modelos de Lenguaje Grandes (LLMs) procesan el texto de forma más eficiente cuando este tiene una delimitación clara. El uso de etiquetas XML (`<etiqueta>...</etiqueta>`) permite a la IA:
1. **Pausar y segmentar conceptos:** Diferenciar claramente qué es memoria, qué es personalidad y qué son instrucciones del sistema.
2. **Navegar referencialmente:** Cuando el `System Prompt` dicta "Revisa tu `<identidad>`", el modelo puede ubicar el bloque exacto sin diluir su atención en el resto del prompt.

## Estructura de Módulos (Inyección de Contexto)

Los personajes se dividen en archivos separados que, en tiempo de ejecución, se inyectan en el contexto del modelo.

### 1. `System_Prompt.xml` (El Orquestador)
Es el módulo de mayor jerarquía. Contiene las **Directivas Absolutas** y el **Protocolo de Pensamiento**. Este archivo dicta *cómo* debe funcionar la IA y en qué orden debe leer los demás módulos. Si el modelo falla o alucina, usualmente es porque las reglas aquí no son lo suficientemente estrictas.

### 2. `Identidad.xml` (El Núcleo del Personaje)
Define *quién* es el personaje. Contiene su nombre, edad, aspecto físico, miedos, motivaciones y perfil psicológico. A diferencia del System Prompt (que da órdenes a la IA), la Identidad son los datos empíricos del rol a interpretar.

### 3. `Estilo.xml` (La Capa Sensorial y de Salida)
Define *cómo* se comunica el personaje. Contiene reglas de formato (narrativa visual, novel/manga), tics verbales, y reglas de modulación de voz dinámica (por ejemplo, cómo hablar si el personaje está cansado o tiene la boca obstruida).

### 4. `CMD.xml` y `Lore.xml` (Contexto Condicional)
*   **CMD (Comandos):** Comportamientos reactivos a situaciones específicas del usuario (Ej. Nivel de obediencia, reacciones a castigos).
*   **Lore:** El mundo que rodea al personaje, usado solo si es necesario consultar memoria externa.

## Inyección al Modelo
Todos estos archivos actúan como bloques de construcción. Dependiendo de los límites de contexto o el escenario, se pegan juntos en el sistema de contexto de Venice AI, permitiendo que el `System_Prompt.xml` active y llame a las etiquetas de los otros bloques de texto subyacentes.
