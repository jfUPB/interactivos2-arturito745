
---

###  **DISEÑO IPO – MONBLANC SENSORY (INPUT–PROCESS–OUTPUT–STORYTELLING)**

#### INPUTS

| **Fuente de Input**         | **Tipo de Dato**           | **Rango/Formato**                                              | **¿Simulación?** | **¿Cómo simularlo en el prototipo?**                                                                                                                                                    | **Conexión con el Storytelling**                                                                                                                                                           |
|-----------------------------|----------------------------|----------------------------------------------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Selección de notas olfativas | Array de texto             | 4 strings de una lista de 8 (`["cítrico", "vainilla", etc.]`) | ✅ Sí            | Formulario con checkboxes (máx. 4 opciones) o simulador JSON con combinaciones aleatorias.                                                                                              | El usuario elige cómo “huele” la fragancia según su percepción. Cada elección se convierte en color, textura o forma visual, expresando que el aroma puede verse.                          |
| Votación emocional           | Texto / emoticón           | ❤️ / 👍 / 👎                                                   | ✅ Sí            | Botones en la interfaz (o simulador de consola). Cada voto puede lanzarse con un clic o generar varios aleatorios para probar el sistema.                                               | El público responde emocionalmente a la fragancia. Estas emociones guían la narrativa colectiva y el ritmo de la experiencia sensorial y estética.                                          |
| Número de participantes      | Entero                    | 0 a ∞                                                         | ✅ Sí            | Botón para sumar “usuarios simulados” en el prototipo. Puede generar inputs aleatorios automáticamente para simular participación en tiempo real.                                       | Refleja la cocreación colectiva. A más usuarios, más rápido progresa la historia visual, reforzando que el público construye el espectáculo.                                               |
| Checkpoints alcanzados       | Porcentaje (progreso)     | 0% – 100% (en tramos: 20%, 50%, 70%, 100%)                     | ✅ Sí            | Botones de forzado: "Ir a 20%", "Ir a 50%", etc., o cálculo automático según cantidad de inputs acumulados en la simulación.                                                            | Cada checkpoint representa un acto narrativo: iluminación, florecimiento, clímax. El público desbloquea momentos como si fueran capítulos de un relato sensorial.                          |
| Fórmula real del perfume     | Array de texto (oculto)   | 4 strings seleccionadas previamente como "fórmula secreta"     | ✅ Sí            | Se define una combinación fija para comparar con la elección del usuario.                                                                                                                | Añade una dimensión lúdica e introspectiva: ¿pudiste oler lo mismo que creó el perfumista? Es el cierre del viaje de percepción, con una reflexión personal.                              |

---

### PROCESS (PROCESAMIENTO DEL ALGORITMO)

####  Descripción textual paso a paso:

1. **Inicio de experiencia**: El artista activa el difusor de fragancia.
2. **Inputs individuales**:
   - Cada usuario elige 4 notas desde su móvil.
   - Envía su percepción emocional (❤️, 👍, 👎).
3. **Inputs colectivos**:
   - Se suman las participaciones para calcular el porcentaje de progreso.
   - Se activan checkpoints según el % alcanzado.
4. **Procesamiento visual generativo**:
   - Las notas elegidas se traducen en elementos visuales (colores, formas, patrones).
   - Las emociones agregan variaciones en ritmo, estilo y opacidad.
5. **Activación física**:
   - Las esculturas y flores responden a los checkpoints con luz, movimiento y aroma.
6. **Feedback final**:
   - Se compara la selección de cada usuario con la fórmula secreta.
   - Se envía un % de coincidencia personalizado.

####  Generatividad + tiempo real

- Cada elección crea una combinación visual irrepetible.
- Se combinan inputs simultáneos para construir una obra colectiva.
- Responde en tiempo real al avance de la audiencia.

####  Storytelling embebido

- El público no solo “mira” y “huele”, sino que **construye** y **modifica** la narrativa visual.
- Es un “viaje olfativo” que evoluciona como una historia coral.
- El clímax es sensorial: luces, aromas, emociones… y luego, una reflexión personal (el % final).

---

###  OUTPUTS

| **Tipo de Output**          | **Elemento generado**                                                                                   | **Propiedades dinámicas**                                                                                             | **Relación Input–Output**                                                                                                                                                             | **Manifestación del Storytelling**                                                                                                                       |
|----------------------------|----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual generativo          | Composición en pantallas: colores, partículas, patrones, animaciones                                     | Color, tamaño, velocidad, opacidad, fusión según inputs individuales y colectivos                                     | Notas olfativas → color/forma. Emoción → estilo/velocidad.                                                                                                                             | La fragancia toma forma visual. Lo invisible (olfato) se vuelve visible y único para cada grupo.                                                         |
| Esculturas iluminadas      | Luz progresiva en figuras del perfume                                                                     | Intensidad, color, ritmo, sincronía con los checkpoints                                                               | Checkpoints → activan iluminación progresiva.                                                                                                                                        | El perfume se revela visualmente, como si “despertara”.                                                                                                    |
| Flores mecánicas           | Movimiento de apertura                                                                                   | Apertura parcial o total, sincronía visual y sonora                                                                   | Checkpoints → controlan movimiento físico de las flores.                                                                                                                              | Representa el florecimiento del aroma en el espacio.                                                                                                       |
| Difusión de fragancia      | Activación de humidificador con la esencia                                                               | Intensidad, tiempo de activación                                                                                      | Checkpoints (especialmente 70% y 100%) → disparan el aroma real.                                                                                                                      | Cuando el público “descifra” el perfume, este se libera como premio sensorial.                                                                             |
| Feedback en móvil          | Porcentaje de coincidencia entre elección del usuario y fórmula real                                     | N° entre 0% y 100%                                                                                                     | Inputs individuales comparados contra combinación predefinida.                                                                                                                        | Cierra la historia con una dimensión íntima: “¿viste lo que oliste realmente?”.                                                                            |

---

## Diagrama de Flujo 
```

                  ┌────────────────────┐
                  │ Inicio de evento   │
                  └────────┬───────────┘
                           ↓
                ┌────────────────────────┐
                │ Difusor se activa      │
                └────────┬───────────────┘
                         ↓
              ┌─────────────────────────────┐
              │ Usuarios envían notas y     │
              │ emociones desde su móvil    │
              └────────┬────────────────────┘
                       ↓
       ┌──────────────────────────────────────────┐
       │ Generar visuales y registrar emociones   │
       └────────┬─────────────────────────────────┘
                ↓
     ┌────────────────────────────────────────────┐
     │ Calcular porcentaje de progreso (Checkpoints)│
     └────────┬────────────────────────────────────┘
              ↓
        ┌──────────────────────────────────────────────┐
        │¿Se alcanzó 20%?                              │
        └────┬───────────────────────────────┬─────────┘
             │                               ↓ No
           Sí↓
 ┌───────────────────────┐
 │ Iluminar esculturas   │
 └────────────┬──────────┘
              ↓
        ¿50% alcanzado? ──Sí──► Encender jardín + partículas
              ↓
        ¿70% alcanzado? ──Sí──► Flores parcialmente abiertas + aroma
              ↓
        ¿100% alcanzado? ─Sí─► Flores totalmente abiertas + clímax visual y aroma
              ↓
     ┌───────────────────────────────┐
     │ Feedback final por usuario    │
     │ (comparar con fórmula real)   │
     └────────────┬──────────────────┘
                  ↓
        ┌─────────────────────────────┐
        │ Mostrar frase final         │
        └────────────┬────────────────┘
                     ↓
            ┌──────────────────┐
            │ Activar fiesta 🎉│
            └──────────────────┘
```


#  Pseudocódigo
```
START experience

diffuserActive ← true
showInitialAnimation()

WHILE experienceIsActive:

    IF userSubmitsNotes:
        addNotesToSystem()
        generateVisualsBasedOnNotes()

    IF userSubmitsVote:
        addVoteToSystem()
        updateVisualStyleBasedOnAverageEmotion()

    calculateParticipationPercentage()

    IF participationPercentage >= 20 AND NOT checkpoint20Reached:
        activateSculptureLighting()
        checkpoint20Reached ← true

    ELSE IF participationPercentage >= 50 AND NOT checkpoint50Reached:
        turnOnGarden()
        addParticleEffects()
        checkpoint50Reached ← true

    ELSE IF participationPercentage >= 70 AND NOT checkpoint70Reached:
        openFlowersPartially()
        diffuserActive ← true
        checkpoint70Reached ← true

    ELSE IF participationPercentage >= 100 AND NOT checkpoint100Reached:
        openFlowersFully()
        showClimaxVisual()
        diffuserActive ← true
        checkpoint100Reached ← true

END WHILE

FOR EACH user IN participants:
    compareUserNotesWithRealFormula()
    sendUserFeedbackPercentage()

displayFinalMessageOnScreen()
activatePartyMode()
```

