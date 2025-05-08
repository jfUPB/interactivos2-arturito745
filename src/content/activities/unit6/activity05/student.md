
# **Blueprint Algorítmico - Unidad 6**

## **Resumen del concepto y narrativa**

Diseñamos una experiencia generativa interactiva en la que el usuario, como un DJ sensorial, mezcla notas olfativas y emociones humanas para crear paisajes visuales que evolucionan en tiempo real. La narrativa se construye a través de "checkpoints emocionales", donde cada decisión afecta el entorno visual como si se tratara de una mezcla en vivo. El sistema responde dinámicamente, transformando los inputs sensoriales en una progresión visual con sentido narrativo, como si estuviéramos frente a una sesión audiovisual que evoluciona al ritmo del usuario.

---

## **Inputs detallados (con detalles de simulación)**

| **Input**                    | **Tipo**          | **Forma de Simulación**                             | **Rango / Valores**                               | **Método**                                        |
|-----------------------------|-------------------|-----------------------------------------------------|---------------------------------------------------|--------------------------------------------------|
| Nota olfativa seleccionada  | Categórico        | Selector simulado mediante botón                    | ["Cítrica", "Amaderada", "Floral", "Especiada"]   | `random()` con probabilidad ponderada por escena |
| Emoción seleccionada        | Categórico        | Selector o `random()` simulando entrada emocional   | ["Alegría", "Tristeza", "Calma", "Ira"]           | random() o input directo desde botón             |
| Intensidad emocional        | Numérico continuo | Slider o `noise()`                                  | 0.0 – 1.0                                         | `noise(frameCount * factor)`                     |
| Checkpoint alcanzado        | Booleano          | Simulado por evento de tiempo o botón manual        | true / false                                      | Activación manual o automática con `millis()`    |
| Participantes activos       | Entero            | Valor simulado constante o dinámico                 | 1 – 10                                            | `random(1, 10)`                                  |
| Dominancia de mezcla        | Calculado         | Emergiendo del sistema al combinar inputs           | Derivado de los valores de entrada                | No se simula directamente                        |

**Activación/Desactivación de Simulación:**
```javascript
let usarSimulacion = true; // Si es true, se generan datos artificiales para pruebas
```

---

## **Proceso (lógica del algoritmo)**

### **Descripción general**

El sistema toma como entradas una nota olfativa y una emoción, junto con su intensidad. A partir de esta combinación, se genera un visual que refleja sensorialmente dicha mezcla. Cuando se alcanza un checkpoint, el sistema identifica la nota dominante en el historial reciente y ejecuta una transición visual intensa (explosión, inversión de parámetros visuales). Esto crea una narrativa de evolución visual, reforzando la relación entre decisiones del usuario y la estética resultante. Cada checkpoint es un punto de inflexión que marca un "acto" dentro del set visual.

### **Pseudocódigo**

```javascript
if (usarSimulacion) {
  nota = random(["Cítrica", "Amaderada", "Floral", "Especiada"]);
  emocion = random(["Alegría", "Tristeza", "Calma", "Ira"]);
  intensidad = noise(frameCount * 0.01);
}

fusión = combinarInputs(nota, emocion, intensidad);
visual = generarVisual(fusión);

if (checkpointAlcanzado) {
  notaDominante = calcularNotaDominante();
  aplicarExplosiónVisual(notaDominante);
  invertirParámetroClave(); // escala, rotación, ruido, color
}

render(visual);
```

### **Lógica de generación visual (detalles clave)**

- La visualización responde directamente a los parámetros de entrada:
  - **Color** según la nota olfativa
  - **Movimiento** según la intensidad emocional
  - **Forma** según el tipo de emoción
- Se utilizan curvas de `noise()` para lograr cambios suaves, y `random()` en momentos específicos para explosiones visuales no predecibles.
- La inversión de parámetros clave se realiza tras cada checkpoint (ej: rotación pasa de 0.01 a -0.03, escala se reduce de 1.2 a 0.7, etc.)
- Se genera un sistema de fusión visual que mezcla las características de varias notas en capas o deformaciones (por ejemplo, visuales tipo shader o malla).

---

## **Outputs detallados**

| **Output**                     | **Tipo**                  | **Propiedades dinámicas**                                                                            | **Relación con Inputs**                                   |
|-------------------------------|---------------------------|-------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| Visual principal               | Visual generativo         | Color, forma, velocidad, suavidad, escala                                                            | Derivado de nota + emoción + intensidad                    |
| Fusión visual (composición)   | Visual combinada          | Mezcla de visuales anteriores, basada en frecuencia de aparición                                     | Calculada a partir de inputs recientes                     |
| Explosión visual (checkpoint) | Evento visual especial    | Color dominante, partículas, incremento de brillo, cambio brusco de parámetros                      | Activada por `checkpointAlcanzado == true`                 |
| Transiciones de escena        | Cambios narrativos visuales | Inversión de parámetros, aumento de complejidad, modificación de `noiseDetail`                      | Derivado de progreso (checkpoints y dominancia emocional)  |
| Feedback audiovisual           | Visual rítmico reactivo   | Efectos tipo "acierto", brillo extra, overlays (estilo Guitar Hero cuando se hace algo bien)        | Triggered cuando fusión es “óptima”                        |

---

## **Notas clave y consideraciones finales**

- **Simulación efectiva:** Se diseñó un sistema de simulación integral utilizando `random()` y `noise()` con rangos adecuados para lograr pruebas realistas y útiles.
- **Storytelling algorítmico:** Cada checkpoint actúa como "hito" narrativo, alterando radicalmente la estética y reforzando la progresión del usuario.
- **Diseño tipo DJ/VJ:** El flujo está inspirado en sesiones en vivo, donde las decisiones afectan directamente la energía visual de la "pista".
- **Curvas controladas:** Se prioriza el uso de ruido (noise) para obtener cambios suaves que simulen entradas humanas naturales.
- **Sistema modular:** El diseño permite fácilmente insertar inputs reales (Webcam, sensores, usuarios remotos) para versiones futuras.

---


