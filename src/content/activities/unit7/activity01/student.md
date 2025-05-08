mi-proyecto-unidad7/
```
│
├── public/                  ← Carpeta para cliente p5.js
│   ├── index.html
│   ├── sketch.js
│   ├── style.css
│
├── server.js                ← Servidor con Express y Socket.io
├── package.json             ← Configuración del proyecto Node

```


## 🗂️ Estructura y tecnologías utilizadas en el servidor

### 📁 `/server`

Carpeta raíz del backend de la aplicación.

---

### `package.json`

**¿Qué es?**
Archivo que define el proyecto Node.js y sus dependencias.

**¿Para qué sirve?**

* Maneja los paquetes que necesita tu servidor (`express`, `cors`, `socket.io`.).
* Define scripts útiles como `npm start` o `npm run dev`.

---

### `server.js` o `index.js`

**¿Qué es?**
Archivo principal del servidor. Aquí es donde se configura y lanza.

**¿Qué tecnologías se usan dentro?**

1. **Express**

   * 📦 `npm install express`
   * 🚀 Para crear un servidor web de forma simple.
   * 🛣️ Define rutas HTTP como `GET /` o `POST /votar`.

2. **CORS**

   * 📦 `npm install cors`
   * 🔐 Permite que el frontend (por ejemplo, tu sketch en `p5.js`) pueda comunicarse con el backend sin bloquearse por políticas de seguridad del navegador.

3. **Socket.IO (opcional si lo usaste)**

   * 📦 `npm install socket.io`
   * 🔁 Para comunicación en tiempo real (emitir votos o actualizaciones a múltiples clientes en vivo).

---

### `.gitignore`

**¿Qué es?**
Archivo que indica a Git qué archivos o carpetas ignorar.

**¿Para qué sirve?**
Evita subir cosas como `node_modules` o archivos temporales que no deben compartirse.

---

### `README.md`

**¿Qué es?**
Archivo de documentación.

**¿Para qué sirve?**
Explica cómo instalar, correr y entender el proyecto. Aquí puedes pegar lo que hicimos antes sobre el uso de Codespaces y la explicación de los archivos.

---

##  ¿Por qué se usa esto?

* Para crear una **API** o servicio en tiempo real que recibe votos de usuarios simulados o reales.
* Para conectar visualizaciones (como la de `p5.js`) con datos en tiempo real.
* Para probar y desarrollar rápido en la nube usando GitHub Codespaces sin necesidad de configurar nada localmente.

### Index.html (Desktop)
```
<!DOCTYPE html>
<html lang="en"> <!-- El idioma del documento está configurado en inglés -->
<head>
    <meta charset="UTF-8"> <!-- Define la codificación de caracteres como UTF-8 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0"> <!-- Hace que el sitio sea responsivo -->

    <!-- Carga de la biblioteca p5.js versión 1.11.0 (para crear gráficos interactivos) -->
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>

    <!-- Carga de la biblioteca Socket.IO versión 4.7.5 (para comunicación en tiempo real con el servidor) -->
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>

    <!-- Carga de p5.js versión 1.4.0 desde otro CDN (puede haber conflicto si se usan dos versiones distintas) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>

    <!-- Archivo de lógica principal del cliente desktop: visualización de mezclas con p5.js -->
    <script src="sketch.js"></script>

    <!-- Título que aparece en la pestaña del navegador -->
    <title>Desktop p5.js Application</title>
</head>

<!-- El cuerpo está vacío porque p5.js se encarga de crear el canvas visual dinámicamente -->
<body></body>
</html>
```

### sketch.js (Desktop) - Visualización en tiempo real de mezclas aromáticas con hilos animados
```
let mezclasPosibles = [];
let votos = {};
let colores;
let topMezclas = [];
let tiempoUltimoVoto = 0;
let hilos = [];
const numPuntos = 150;
const separacionTrenzas = 200;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);
  colorMode(RGB, 255, 255, 255, 1);

  // Paleta de colores asociada a cada nota aromática
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
}

function draw() {
  background(0, 0.03);

  if (millis() - tiempoUltimoVoto > 1000) {
    simularVoto();              // Generar votos simulados
    tiempoUltimoVoto = millis();
    calcularTopMezclas();       // Calcular las 2 mezclas más votadas
  }

  actualizarHilos();           // Actualizar los puntos y curvas
  dibujarHilos();              // Dibujar visualmente los hilos
  mostrarVotos();              // Mostrar texto con votos en pantalla
}

// Generar combinaciones posibles de 3 notas
function generarMezclasPosibles() {
  let notas = Object.keys(colores);
  for (let i = 0; i < notas.length; i++) {
    for (let j = i + 1; j < notas.length; j++) {
      for (let k = j + 1; k < notas.length; k++) {
        let mezcla = [notas[i], notas[j], notas[k]];
        let clave = mezcla.join("-");
        mezclasPosibles.push(mezcla);
        votos[clave] = 0;
      }
    }
  }
}

// Inicializa la estructura de los hilos (uno por nota)
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

// Voto simulado aleatorio sobre una mezcla posible
function simularVoto() {
  if (mezclasPosibles.length > 0) {
    let mezcla = random(mezclasPosibles);
    let clave = mezcla.join("-");
    votos[clave]++;
  }
}

// Ordena mezclas por votos y guarda las 2 más votadas
function calcularTopMezclas() {
  let mezclasOrdenadas = Object.entries(votos).sort((a, b) => b[1] - a[1]);
  topMezclas = mezclasOrdenadas.slice(0, 2).map(entry => entry[0].split("-"));
}

// Actualiza lógica y movimiento de los hilos
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

// Define cómo se dibujan las trenzas con movimiento
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

// Dibuja los hilos activos con curvas y círculos al final
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

    // Círculo decorativo al final del hilo
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

// Muestra en pantalla las mezclas más votadas
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

// Asegura que el canvas se adapte al redimensionar la ventana
function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
### Server.js
```

// Importa el framework Express para crear el servidor web
const express = require('express');

// Módulo HTTP de Node.js para crear el servidor
const http = require('http');

// Socket.IO permite comunicación en tiempo real entre cliente y servidor
const socketIO = require('socket.io');

// Inicializa la aplicación Express
const app = express();

// Crea un servidor HTTP a partir de Express
const server = http.createServer(app); 

// Inicializa Socket.IO sobre el servidor HTTP
const io = socketIO(server); 

// Define el puerto donde se ejecutará el servidor
const port = 3000;

// Sirve archivos estáticos desde la carpeta 'public' (por ejemplo, index.html, sketch.js)
app.use(express.static('public'));

// Lista de notas aromáticas disponibles para la mezcla
const notasDisponibles = ['vainilla', 'citricos', 'maderas', 'flores', 'cuero', 'mandarina'];

// Función para generar una mezcla aleatoria de 3 notas sin repetir
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

// Manejo de conexiones con clientes a través de Socket.IO
io.on('connection', (socket) => {
    console.log('New client connected');

    // Recibe mensajes personalizados y los retransmite a los demás clientes
    socket.on('message', (message) => {
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    // Detecta cuando un cliente se desconecta
    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

// Cada 2 segundos, genera y envía una nueva mezcla simulada a todos los clientes
setInterval(() => {
    const mezcla = generarMezclaAleatoria(); // Genera mezcla
    const user = `user${Math.floor(Math.random() * 1000)}`; // Simula nombre de usuario
    io.emit('nuevaMezcla', { user, notas: mezcla }); // Envía mezcla a todos los clientes
    console.log(`Enviando mezcla de ${user}: ${mezcla.join(', ')}`);
}, 2000);

// Inicia el servidor y muestra mensaje en consola
server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```
