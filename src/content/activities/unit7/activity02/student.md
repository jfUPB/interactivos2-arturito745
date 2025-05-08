# Implementación del Núcleo del Proceso y Simulación de Datos

Basado en el código proporcionado de la visualización de mezclas aromáticas, he implementado el núcleo del proceso y la simulación de datos como se describe en el blueprint algorítmico.

## Lógica Principal del Proceso

El proceso central consiste en:
1. Recibir votos simulados sobre combinaciones de notas aromáticas
2. Calcular las mezclas más populares
3. Visualizar estas mezclas como hilos animados que se entrelazan

```javascript
// Proceso principal en draw()
function draw() {
  background(0, 0.03);

  // Paso 1: Simular votos periódicamente
  if (millis() - tiempoUltimoVoto > 1000) {
    simularVoto();              // Generar votos simulados
    tiempoUltimoVoto = millis();
    calcularTopMezclas();       // Calcular las 2 mezclas más votadas
  }

  // Paso 2: Actualizar visualización basada en los votos
  actualizarHilos();           // Actualizar los puntos y curvas
  dibujarHilos();              // Dibujar visualmente los hilos
  mostrarVotos();              // Mostrar texto con votos en pantalla
}
```

## Implementación de la Simulación de Datos

He implementado tres estrategias de simulación diferentes que pueden alternarse:

```javascript
// Variables para controlar la simulación
let estrategiaSimulacion = 1; // 1: aleatoria, 2: tendencia, 3: patron cíclico
let notaFavorita = "vainilla";

function simularVoto() {
  if (mezclasPosibles.length === 0) return;
  
  let mezcla;
  
  // Estrategia 1: Votos completamente aleatorios
  if (estrategiaSimulacion === 1) {
    mezcla = random(mezclasPosibles);
  }
  // Estrategia 2: Votos con tendencia hacia una nota favorita
  else if (estrategiaSimulacion === 2) {
    if (random() > 0.7) {
      // 70% de probabilidad de que contenga la nota favorita
      let mezclasConFavorita = mezclasPosibles.filter(m => m.includes(notaFavorita));
      mezcla = random(mezclasConFavorita.length > 0 ? mezclasConFavorita : mezclasPosibles);
    } else {
      mezcla = random(mezclasPosibles);
    }
  }
  // Estrategia 3: Patrón cíclico que cambia cada 10 segundos
  else if (estrategiaSimulacion === 3) {
    let ciclo = floor(millis() / 10000) % Object.keys(colores).length;
    let notaCiclo = Object.keys(colores)[ciclo];
    let mezclasCiclo = mezclasPosibles.filter(m => m.includes(notaCiclo));
    mezcla = random(mezclasCiclo.length > 0 ? mezclasCiclo : mezclasPosibles);
  }

  let clave = mezcla.join("-");
  votos[clave]++;
  
  // Debug: mostrar información del voto simulado
  console.log(`Voto simulado: ${clave}`, 
              `Estrategia: ${estrategiaSimulacion}`,
              `Total votos: ${votos[clave]}`);
}
```

## Conexión entre Simulación y Proceso

La conexión se realiza a través de:
1. La función `simularVoto()` que actualiza el objeto `votos`
2. La función `calcularTopMezclas()` que procesa estos votos
3. La visualización que reacciona a los cambios en `topMezclas`

```javascript
function calcularTopMezclas() {
  // Convertir votos a array y ordenar
  let mezclasOrdenadas = Object.entries(votos).sort((a, b) => b[1] - a[1]);
  
  // Tomar las 2 primeras (o menos si no hay suficientes)
  topMezclas = mezclasOrdenadas.slice(0, 2).map(entry => entry[0].split("-"));
  
  // Debug: mostrar top mezclas
  console.log("Top mezclas actualizado:", 
              topMezclas.map(m => m.join("-")), 
              "con votos:", 
              topMezclas.map(m => votos[m.join("-")]));
}
```

## Salidas de Prueba

Ejemplo de salidas en consola durante la simulación:

```
Voto simulado: vainilla-citricos-maderas Estrategia: 1 Total votos: 1
Top mezclas actualizado: ["vainilla-citricos-maderas"] con votos: [1]

Voto simulado: flores-cuero-mandarina Estrategia: 1 Total votos: 1
Top mezclas actualizado: ["vainilla-citricos-maderas", "flores-cuero-mandarina"] con votos: [1, 1]

Voto simulado: vainilla-citricos-maderas Estrategia: 2 Total votos: 2
Top mezclas actualizado: ["vainilla-citricos-maderas", "flores-cuero-mandarina"] con votos: [2, 1]
```

## Desafíos y Soluciones

1. **Desafío**: Las transiciones entre mezclas eran muy abruptas.
   - **Solución**: Implementé un sistema de progreso suave en `actualizarHilos()` usando lerp() y variables de progreso.

2. **Desafío**: La simulación aleatoria pura no mostraba patrones interesantes.
   - **Solución**: Agregué múltiples estrategias de simulación que pueden alternarse para probar diferentes escenarios.

3. **Desafío**: El cálculo de las mezclas top podía fluctuar demasiado.
   - **Solución**: Implementé un sistema de votos acumulativos en lugar de reiniciar los contadores cada vez.

Esta implementación proporciona una base sólida para el sistema de visualización, con una clara separación entre la lógica del proceso, la simulación de datos y la visualización, permitiendo probar diferentes escenarios y comportamientos del sistema.
