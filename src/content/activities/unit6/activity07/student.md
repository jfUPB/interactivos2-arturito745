Aquí tienes el esquema completo de la actividad **“Preparación para la implementación (Planificación)”** redactado en **primera persona**, con tono técnico y estructurado, listo para tu bitácora de estudiante:

---

# **Preparación para la implementación (Planificación)**  
**Unidad 6 – Reflexión y Planificación para Unidad 7**

## **1. Reflexión sobre el proceso de diseño**

Durante esta unidad, la parte más intuitiva para mí fue definir los **Outputs** y conectar el **Storytelling** con la visualización. Desde el principio tenía una imagen clara del tipo de experiencia que quería: una mezcla en vivo de notas olfativas y emociones que se tradujera visualmente como una sesión DJ/VJ sensorial. Me resultó natural imaginar cómo los inputs emocionales se manifestarían en formas, colores y comportamientos dinámicos, inspirándome en herramientas como TouchDesigner y conciertos de música electrónica.

La parte más desafiante fue estructurar el **Proceso algorítmico** de forma lógica y traducible a código. Tenía muchas ideas sueltas (inversión de parámetros, checkpoints, explosiones visuales), pero ordenarlas como un flujo claro y modular no fue inmediato. Para abordarlo, primero redacté la narrativa completa como si fuese una experiencia escénica, luego identifiqué los eventos clave (como los checkpoints), y por último reorganicé cada comportamiento visual dentro de esos puntos narrativos. Usé pseudocódigo y tablas para clarificar la lógica detrás de cada transición.

---

## **2. Primeros pasos concretos de implementación en Unidad 7**

1. **Configurar el sketch base en p5.js**: establecer el entorno básico con funciones `setup()` y `draw()`, y crear las variables necesarias para simular los inputs definidos (nota, emoción, intensidad, checkpoint).
2. **Implementar la simulación de inputs**: programar los generadores de datos usando `random()` y `noise()` según lo definido en el blueprint. También incorporar sliders para tener control manual durante las pruebas.
3. **Prototipar la visualización básica**: codificar una primera versión del motor visual que responda directamente a los inputs simulados, usando formas, colores y movimientos básicos. Este paso me permitirá validar que el flujo Input -> Output esté funcionando correctamente antes de agregar complejidad.

---

## **3. Preguntas pendientes**

- ¿Cuál es la mejor manera en p5.js de organizar código modular para cada etapa visual (por ejemplo, usar clases para cada tipo de nota/emoción)?
- ¿Cómo puedo detectar visualmente si una combinación específica de inputs está generando una mezcla “óptima”? ¿Necesito definir un umbral o patrón específico?
- ¿Cuál es la forma más eficiente de guardar un historial corto de inputs anteriores (por ejemplo, para detectar la nota dominante en los últimos 10 segundos)?
- ¿Puedo usar blendModes o shaders personalizados en p5.js para crear efectos de fusión más ricos, sin comprometer el rendimiento?
- ¿Cómo podría extender este sistema en el futuro para trabajar en red (WebSockets) si quisiera recibir inputs de varios usuarios en tiempo real?

---

## **4. Gestión del tiempo (Unidad 7)**

Reconozco que la Unidad 7 implicará bastante codificación, ajustes y pruebas visuales. Para gestionarlo eficientemente, decidí aplicar las siguientes estrategias:

- **Bloques de trabajo de 90 minutos diarios**, dedicados exclusivamente al desarrollo del proyecto. Usaré técnicas como Pomodoro para mantener la concentración.
- **Avanzar primero en lo que está más claro y definido** (inputs simulados y visualización inicial), y dejar para después los efectos más complejos como las explosiones visuales de checkpoint.
- **Guardar versiones parciales del sketch** cada vez que cierre una funcionalidad, para poder volver fácilmente si algo se rompe.
- **Pedir ayuda temprana si me estanco**, especialmente en temas como blending o historial de datos.
- **Mantener una bitácora de desarrollo paralela**, donde registre errores, ideas espontáneas y decisiones de diseño en cada sesión de programación.
