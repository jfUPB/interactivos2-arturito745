# Exploración Conceptual: "¿Qué Pasaría Si...?" para el Sistema de Visualización de Mezclas Aromáticas

## 1. Inputs Extremos

**Escenario**: ¿Qué pasaría si recibimos una cantidad masiva de votos simultáneos (pico de tráfico) o ningún voto durante un período prolongado?

**Comportamiento esperado**:
- Con muchos votos simultáneos: El sistema podría saturarse temporalmente, especialmente si el servidor no está optimizado para manejar múltiples conexiones Socket.IO simultáneas. Las visualizaciones podrían volverse menos fluidas mientras procesa todos los votos.
- Sin votos: Las visualizaciones seguirían mostrando las últimas mezclas populares, pero eventualmente se "apagarían" cuando los hilos inactivos alcancen progreso 0.

**Reflexión**: 
- Es deseable mantener cierta persistencia visual incluso sin nuevos votos. Podría implementarse un "modo espera" con animaciones mínimas cuando no hay actividad.
- Para manejar picos de tráfico, deberíamos considerar limitar la tasa de votos por cliente y optimizar el servidor.

## 2. Cambio de Parámetro Interno

**Escenario**: ¿Qué pasaría si modificamos el parámetro que controla la velocidad de aparición/desaparición de los hilos (actualmente 0.01 para aparecer y 0.02 para desaparecer)?

**Comportamiento esperado**:
- Aumentando estos valores: Los hilos responderían más rápido a los cambios en las mezclas populares, creando una experiencia más dinámica pero potencialmente caótica.
- Disminuyendo estos valores: Las transiciones serían más suaves pero podrían percibirse como lentas o poco responsivas.

**Reflexión**:
- Los valores actuales parecen equilibrados. Una opción interesante sería hacer que estos parámetros sean configurables desde el cliente móvil, permitiendo ajustar el "estado de ánimo" de la visualización.

## 3. Combinación de Inputs

**Escenario**: ¿Qué pasaría si el cliente móvil envía votos consistentes para una misma mezcla mientras otros clientes votan aleatoriamente?

**Comportamiento esperado**:
- La mezcla votada consistentemente dominaría rápidamente una de las posiciones "top", mostrando un hilo estable y prominente.
- La otra posición "top" mostraría cambios más dinámicos según los votos aleatorios de otros clientes.

**Reflexión**:
- Este comportamiento es deseable ya que refleja tanto la consistencia como la diversidad de preferencias.
- Podríamos mejorar destacando visualmente las mezclas que reciben votos consecutivos del mismo cliente.

## 4. Falla de Input

**Escenario**: ¿Qué pasaría si el servidor deja de recibir datos del cliente móvil?

**Comportamiento esperado**:
- Actualmente, el sistema tiene votos simulados como respaldo, por lo que la visualización continuaría funcionando.
- Sin el respaldo de votos simulados, las visualizaciones eventualmente se desvanecerían al no haber nuevas mezclas para mostrar.

**Reflexión**:
- Es importante mantener algún mecanismo de respaldo (como los votos simulados) para casos de falla.
- Podríamos implementar un estado de "conexión perdida" que notifique visualmente al usuario desktop sobre la interrupción.

## Implementación de Comunicación Mobile-Desktop

Para conectar el cliente móvil con el desktop a través del servidor, necesitamos modificar ligeramente los scripts existentes:

1. **Modificación en server.js**:
```javascript
// En el manejador de conexiones Socket.IO
io.on('connection', (socket) => {
    console.log('New client connected');

    // Recibe votos desde clientes móviles
    socket.on('votoDesdeMobile', (mezcla) => {
        console.log(`Voto recibido desde móvil: ${mezcla.join(', ')}`);
        // Transmitir a todos los clientes desktop
        io.emit('nuevaMezcla', { 
            user: 'mobileUser', 
            notas: mezcla 
        });
    });

    // Resto del código existente...
});
```

2. **Cliente Mobile (sketch.js modificado)**:
```javascript
// Función simulada para enviar votos desde el móvil
function enviarVotoMobile(mezcla) {
    socket.emit('votoDesdeMobile', mezcla);
}

// Ejemplo de uso - esto podría activarse con botones en la UI móvil
enviarVotoMobile(['vainilla', 'citricos', 'flores']);
```

3. **Cliente Desktop (sketch.js existente)**:
- Ya está preparado para recibir las mezclas a través del evento 'nuevaMezcla' y procesarlas en el sistema de votación.

Esta implementación permite que el móvil envíe mezclas específicas que luego serán visualizadas en el desktop, complementando o reemplazando los votos simulados según sea necesario.


### Codigos  de la API


# Códigos completos implementados para el sistema Mobile-Desktop

## 1. server.js (Servidor actualizado)

```javascript
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

app.use(express.static('public'));

const notasDisponibles = ['vainilla', 'citricos', 'maderas', 'flores', 'cuero', 'mandarina'];

function generarMezclaAleatoria() {
    const mezcla = [];
    const seleccionadas = new Set();
    while (mezcla.length < 3) {
        const nota = notasDisponibles[Math.floor(Math.random() * notasDisponibles.length)];
        if (!seleccionadas.has(nota)) {
            mezcla.push(nota);
            seleccionadas.add(nota);
        }
    }
    return mezcla;
}

// Almacén de votos
const votosGlobales = {};

io.on('connection', (socket) => {
    console.log('New client connected');

    // Manejar votos desde móvil
    socket.on('votoDesdeMobile', (mezcla) => {
        const clave = mezcla.join('-');
        votosGlobales[clave] = (votosGlobales[clave] || 0) + 1;
        console.log(`Voto recibido desde móvil: ${clave}`);
        io.emit('actualizarVotos', votosGlobales);
    });

    // Enviar estado inicial al cliente que se conecta
    socket.emit('actualizarVotos', votosGlobales);

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

// Simular votos aleatorios para cuando no hay móviles conectados
setInterval(() => {
    if (Object.keys(io.sockets.sockets).length > 0) {
        const mezcla = generarMezclaAleatoria();
        const clave = mezcla.join('-');
        votosGlobales[clave] = (votosGlobales[clave] || 0) + 1;
        io.emit('actualizarVotos', votosGlobales);
        console.log(`Voto simulado: ${clave}`);
    }
}, 3000);

server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```

## 2. Desktop Files

### index.html (Desktop)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <script src="sketch-desktop.js"></script>
    <title>Desktop Visualizer</title>
    <style>
        body { margin: 0; overflow: hidden; }
    </style>
</head>
<body></body>
</html>
```

### sketch-desktop.js

```javascript
let mezclasPosibles = [];
let votos = {};
let colores;
let topMezclas = [];
let tiempoUltimoVoto = 0;
let hilos = [];
const numPuntos = 150;
const separacionTrenzas = 200;
let socket;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);
  colorMode(RGB, 255, 255, 255, 1);

  colores = {
    "vainilla": color(255, 250, 205),
    "citricos": color(144, 238, 144),
    "maderas": color(139, 69, 19),
    "flores": color(147, 112, 219),
    "cuero": color(62, 39, 35),
    "mandarina": color(255, 165, 0)
  };

  generarMezclasPosibles();
  inicializarHilos();

  // Configurar Socket.IO
  socket = io();
  socket.on('actualizarVotos', (nuevosVotos) => {
    votos = nuevosVotos;
    calcularTopMezclas();
  });
}

function draw() {
  background(0, 0.03);
  actualizarHilos();
  dibujarHilos();
  mostrarVotos();
}

function generarMezclasPosibles() {
  let notas = Object.keys(colores);
  for (let i = 0; i < notas.length; i++) {
    for (let j = i + 1; j < notas.length; j++) {
      for (let k = j + 1; k < notas.length; k++) {
        let mezcla = [notas[i], notas[j], notas[k]];
        let clave = mezcla.join("-");
        mezclasPosibles.push(mezcla);
        if (!votos[clave]) votos[clave] = 0;
      }
    }
  }
}

function inicializarHilos() {
  for (let i = 0; i < 6; i++) {
    hilos[i] = {
      puntos: [],
      progreso: 0,
      activo: false,
      indiceNota: i
    };
    for (let j = 0; j < numPuntos; j++) {
      hilos[i].puntos[j] = {
        x: (width / numPuntos) * j,
        y: height / 2,
        targetX: (width / numPuntos) * j,
        targetY: height / 2
      };
    }
  }
}

function calcularTopMezclas() {
  let mezclasOrdenadas = Object.entries(votos).sort((a, b) => b[1] - a[1]);
  topMezclas = mezclasOrdenadas.slice(0, 2).map(entry => entry[0].split("-"));
}

function actualizarHilos() {
  for (let i = 0; i < hilos.length; i++) {
    hilos[i].activo = false;
  }

  if (topMezclas.length > 0) {
    const centroY1 = height / 2 - separacionTrenzas / 2;
    configurarTrenza(topMezclas[0], centroY1, 0.05, frameCount * 0.03);

    if (topMezclas.length > 1) {
      const centroY2 = height / 2 + separacionTrenzas / 2;
      configurarTrenza(topMezclas[1], centroY2, 0.05, frameCount * 0.03 + PI);
    }
  }

  for (let i = 0; i < hilos.length; i++) {
    if (hilos[i].activo) {
      hilos[i].progreso = min(hilos[i].progreso + 0.01, 1);
    } else {
      hilos[i].progreso = max(hilos[i].progreso - 0.02, 0);
    }

    for (let j = 0; j < numPuntos; j++) {
      hilos[i].puntos[j].x = lerp(hilos[i].puntos[j].x, hilos[i].puntos[j].targetX, 0.1);
      hilos[i].puntos[j].y = lerp(hilos[i].puntos[j].y, hilos[i].puntos[j].targetY, 0.1);
    }
  }
}

function configurarTrenza(mezcla, centroY, amplitud, tiempoBase) {
  for (let n = 0; n < mezcla.length; n++) {
    const nota = mezcla[n];
    const indiceNota = Object.keys(colores).indexOf(nota);
    if (indiceNota >= 0) {
      hilos[indiceNota].activo = true;
      const retraso = n * 0.3;

      for (let j = 0; j < numPuntos; j++) {
        const progresoPunto = map(j, 0, numPuntos, 0, 1);
        const visible = progresoPunto < hilos[indiceNota].progreso + retraso;

        if (visible) {
          const offsetY = sin(tiempoBase + j * 0.1 + n * 1.5) * amplitud * 200;
          hilos[indiceNota].puntos[j].targetY = centroY + offsetY;
        } else {
          hilos[indiceNota].puntos[j].targetY = centroY + (n % 2 == 0 ? -100 : 100);
        }
      }
    }
  }
}

function dibujarHilos() {
  const nombresNotas = Object.keys(colores);

  for (let i = 0; i < hilos.length; i++) {
    if (hilos[i].progreso <= 0) continue;

    const c = colores[nombresNotas[i]];
    const puntosVisibles = floor(numPuntos * hilos[i].progreso);

    stroke(c);
    strokeWeight(4);
    noFill();

    beginShape();
    for (let j = 0; j < puntosVisibles; j++) {
      curveVertex(hilos[i].puntos[j].x, hilos[i].puntos[j].y);
    }
    endShape();

    if (puntosVisibles > 10) {
      fill(c);
      noStroke();
      circle(
        hilos[i].puntos[puntosVisibles - 1].x,
        hilos[i].puntos[puntosVisibles - 1].y,
        10
      );
    }
  }
}

function mostrarVotos() {
  fill(255);
  textSize(16);
  textAlign(LEFT);
  text("Top mezclas votadas:", 20, 30);

  for (let i = 0; i < topMezclas.length; i++) {
    let clave = topMezclas[i].join("-");
    text(`${clave}: ${votos[clave]} votos`, 20, 60 + i * 20);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

## 3. Mobile Files

### index.html (Mobile)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <script src="sketch-mobile.js"></script>
    <title>Mobile Controller</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            touch-action: manipulation;
            user-select: none;
            -webkit-user-select: none;
        }
        #container {
            display: flex;
            flex-direction: column;
            height: 100vh;
        }
        .button-row {
            display: flex;
            flex: 1;
        }
        .aroma-button {
            flex: 1;
            margin: 5px;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: transform 0.1s;
        }
        .aroma-button:active {
            transform: scale(0.95);
        }
        #selected-container {
            padding: 10px;
            background: #f0f0f0;
            text-align: center;
        }
        #vote-button {
            padding: 15px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 18px;
            margin: 10px;
        }
    </style>
</head>
<body>
    <div id="container">
        <div id="selected-container">
            <h3>Seleccionadas: <span id="selected-display">Ninguna</span></h3>
        </div>
        <div class="button-row">
            <button class="aroma-button" style="background-color: #FFFACD;" data-aroma="vainilla">Vainilla</button>
            <button class="aroma-button" style="background-color: #90EE90;" data-aroma="citricos">Cítricos</button>
        </div>
        <div class="button-row">
            <button class="aroma-button" style="background-color: #8B4513;" data-aroma="maderas">Maderas</button>
            <button class="aroma-button" style="background-color: #9370DB;" data-aroma="flores">Flores</button>
        </div>
        <div class="button-row">
            <button class="aroma-button" style="background-color: #3E2723; color: white;" data-aroma="cuero">Cuero</button>
            <button class="aroma-button" style="background-color: #FFA500;" data-aroma="mandarina">Mandarina</button>
        </div>
        <button id="vote-button">VOTAR MEZCLA</button>
    </div>
</body>
</html>
```

### sketch-mobile.js

```javascript
let selectedAromas = [];
let socket;

document.addEventListener('DOMContentLoaded', () => {
    // Configurar Socket.IO
    socket = io();
    
    // Configurar botones de aromas
    const aromaButtons = document.querySelectorAll('.aroma-button');
    aromaButtons.forEach(button => {
        button.addEventListener('click', () => {
            const aroma = button.getAttribute('data-aroma');
            
            if (selectedAromas.includes(aroma)) {
                // Si ya está seleccionado, quitarlo
                selectedAromas = selectedAromas.filter(a => a !== aroma);
                button.style.border = 'none';
            } else if (selectedAromas.length < 3) {
                // Si hay menos de 3 seleccionados, agregarlo
                selectedAromas.push(aroma);
                button.style.border = '3px solid black';
            }
            
            updateSelectedDisplay();
        });
    });
    
    // Configurar botón de votar
    document.getElementById('vote-button').addEventListener('click', () => {
        if (selectedAromas.length === 3) {
            socket.emit('votoDesdeMobile', selectedAromas);
            
            // Feedback visual
            const voteButton = document.getElementById('vote-button');
            voteButton.textContent = '✓ Votado!';
            voteButton.style.backgroundColor = '#2E7D32';
            
            setTimeout(() => {
                voteButton.textContent = 'VOTAR MEZCLA';
                voteButton.style.backgroundColor = '#4CAF50';
            }, 2000);
        } else {
            alert('Por favor selecciona exactamente 3 aromas');
        }
    });
});

function updateSelectedDisplay() {
    const display = document.getElementById('selected-display');
    
    if (selectedAromas.length === 0) {
        display.textContent = 'Ninguna';
    } else {
        display.textContent = selectedAromas.join(', ');
    }
    
    // Resetear bordes de todos los botones
    document.querySelectorAll('.aroma-button').forEach(button => {
        button.style.border = selectedAromas.includes(button.getAttribute('data-aroma')) 
            ? '3px solid black' 
            : 'none';
    });
}
```

## Estructura de archivos recomendada

```
/proyecto-aromas
│
├── /public
│   ├── /desktop
│   │   ├── index.html
│   │   └── sketch-desktop.js
│   │
│   ├── /mobile
│   │   ├── index.html
│   │   └── sketch-mobile.js
│   │
│   └── /shared
│       └── (archivos compartidos si los hay)
│
└── server.js
```

## Instrucciones para ejecutar:

1. Instalar dependencias:
```bash
npm init -y
npm install express socket.io
```

2. Iniciar el servidor:
```bash
node server.js
```

3. Acceder desde:
- Desktop: http://localhost:3000/desktop/
- Mobile: http://localhost:3000/mobile/

El sistema ahora permite que los usuarios móviles seleccionen combinaciones de aromas y las envíen al servidor, que luego las transmite a la visualización en el desktop. La visualización mostrará las dos combinaciones más votadas como trenzas animadas.
