
### ✅ **1. Inputs a Simular**

| **Input**                   | **Tipo de Dato**               | **¿Requiere Simulación?** | **Razón**                                                  |
|----------------------------|-------------------------------|---------------------------|-------------------------------------------------------------|
| Notas olfativas            | Array de texto (4 de 8)        | ✅ Sí                    | No hay conexión con una base real, se generan al azar.     |
| Votación emocional         | Texto / emoticón               | ✅ Sí                    | El usuario no votará en vivo, se generarán votos ficticios. |
| Número de participantes    | Entero                         | ✅ Sí                    | Se simulará incremento de usuarios para probar visuales.   |
| Checkpoints alcanzados     | Porcentaje (20%, 50%, etc.)    | ✅ Sí                    | Se calculará automáticamente o forzará manualmente.        |
| Fórmula real del perfume   | Array de texto (oculta)        | ✅ Sí                    | Se fija una “fórmula secreta” para pruebas internas.       |

---

### 🧰 **2. Métodos de Simulación en p5.js**

| **Input**                 | **Método de Simulación**                                                                                                                                     |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Notas olfativas**      | `random(notesPool)` → Array de 4 strings únicos desde un array de 8 opciones. Refresca cada X segundos o con un botón.                                        |
| **Votación emocional**   | `random(["❤️", "👍", "👎"])` → Con distribución desigual si se desea (ej: más ❤️). Cambia cada 2-4 segundos o por botón manual.                                 |
| **Número de participantes** | Usar `frameCount % 120 == 0` para sumar aleatoriamente entre 1 y 3 usuarios. O `slider` para control manual.                                                |
| **Checkpoints**          | Se calcula automáticamente a partir de la cantidad de participantes, o con botones forzados ("Ir a 20%", "Ir a 50%", etc.).                                   |
| **Fórmula del perfume**  | Definida como `const formula = ["cítrico", "vainilla", "rosa", "madera"]`. Se compara con las notas olfativas simuladas para simular un "porcentaje de match". |

---

### 🧠 **3. Comportamiento Simulado**

| **Input**                 | **Comportamiento Buscado**                                                                                          |
|--------------------------|----------------------------------------------------------------------------------------------------------------------|
| Notas olfativas           | Cambios *espaciados y variados* (cada 5-10 segundos), simulando decisiones individuales.                            |
| Votación emocional        | *Picos aleatorios ocasionales* de “❤️” o “👎” como reacción variable a una “fragancia”.                              |
| Número de participantes   | *Crecimiento progresivo* con subidas y pausas, usando `noise()` para hacerlo orgánico.                              |
| Checkpoints               | *Desbloqueo progresivo* con transiciones visuales notorias al cambiar de 20% → 50% → 70% → 100%.                    |
| Fórmula del perfume       | *Match dinámico* con visualización de porcentaje (ej: 60% de coincidencia genera una visual más “calmada”).         |

---

### 🕹️ **4. Controles Manuales en el Prototipo**

Sí, incluiremos:

- ✅ **Sliders**: para ajustar manualmente la cantidad de participantes (de 0 a 100).
- ✅ **Botones**: para forzar un cambio de checkpoint o de votación emocional.
- ✅ **Checkbox de activación**: variable `usarSimulacion = true/false` para alternar entre simulación y control manual.

---

### 🧯 **5. Activación/Desactivación de Simulación**

```js
let usarSimulacion = true;

function draw() {
  if (usarSimulacion) {
    simularInputs(); // llama a la función de simulación
  } else {
    // modo manual, controlado por sliders y botones
  }
}
```

Esto nos permite:

- Probar el sistema en *modo demo* con auto-generación.
- Usar *modo test* donde se controla todo desde UI de p5.js.

---
