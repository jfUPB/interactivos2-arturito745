#####
## Cambio en los mesajes de consola 

### consola
```
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {

    console.log('Nuevo cliente conectado');
    socket.on('message', (message) => {
       console.log(`Received message => ${message}`);
      socket.broadcast.emit('message', message);
    });

   socket.on('disconnect', () => {
      console.log('Cliente desconectado');
    });
});



server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});

```

Este cambio se hizo en el archivo server.js, hice cambios en las lineas console.log

## Cambios en los datos modificacion en los datos enviados eñadimos nuevos datos 



## server.js (Registra y envía la hora de conexión/desconexión)

```
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    let nombre = `Cliente-${Math.floor(Math.random() * 1000)}`;
    let horaConexion = new Date().toLocaleTimeString();

    console.log(`🟢 [${horaConexion}] ${nombre} conectado`);
    io.emit("hora_conexion", { usuario: nombre, hora: horaConexion });

    socket.on('disconnect', () => {
        let horaDesconexion = new Date().toLocaleTimeString();
        console.log(`🔴 [${horaDesconexion}] ${nombre} se desconectó.`);
        io.emit("hora_desconexion", { usuario: nombre, hora: horaDesconexion });
    });
});

server.listen(port, () => console.log(`🚀 Servidor en http://localhost:${port}`));
```
###  (Reciben y muestran en consola) 
**Ubicación:** `public/desktop/sketch.js` y `public/mobile/sketch.js`  

```js
let socket;
function setup() {
    createCanvas(400, 400);
    socket = io("http://localhost:3000");

    socket.on("hora_conexion", (data) => console.log(`🟢 ${data.usuario} conectado a las ${data.hora}`));
    socket.on("hora_desconexion", (data) => console.log(`🔴 ${data.usuario} desconectado a las ${data.hora}`));
}

function draw() {
    background(220);
    textAlign(CENTER, CENTER);
    textSize(20);
    text("Esperando conexión...", width / 2, height / 2);
}
```

---

 **Ahora la hora de conexión y desconexión se envía y se ve en la consola.**  
## Type touch 


**Resumen del proceso para quitar `type: 'touch'`**  

 **1️⃣ Eliminamos `type: 'touch'` en `mobile/sketch.js`**  
- **Borramos** `socket.emit('message', JSON.stringify(touchData))` en `touchMoved()`.  
- Ahora `mobile` solo envía `{ x, y }` con `socket.emit("posicion_mouse", { x, y })`.  

 **2️⃣ Eliminamos `socket.on('message')` en `desktop/sketch.js`**  
- **Borramos** la parte donde verificaba `if (parsedData.type === 'touch')`.  
- Ahora `desktop` recibe `posicion_mouse` directamente y actualiza el círculo.  

 **3️⃣ Eliminamos `socket.on("message")` en `server.js`**  
- **Borramos** `socket.on('message', ...)` porque ya no se usa.  
- El servidor ahora solo maneja `posicion_mouse`.  

 **4️⃣ Guardamos y reiniciamos el servidor**  
```sh
npm start
```
 **¡Listo! Ahora `type: 'touch'` desapareció y el código es más limpio.** 🎉
Aquí están los **códigos modificados** después de eliminar `type: 'touch'`:  

---

## **📌 1️⃣ `mobile/sketch.js` (Se eliminó `type: 'touch'`)**  
📌 **Ubicación:** `public/mobile/sketch.js`  
📌 **Cambios realizados:**  
✅ **Se eliminó `socket.emit('message', JSON.stringify(touchData))`.**  
✅ **Ahora solo envía `{ x, y }` con `socket.emit("posicion_mouse", { x, y })`.**  

🔹 **Código corregido:**  
```js
function touchMoved() {
    if (socket && socket.connected) { 
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold) {
            socket.emit("posicion_mouse", { x: mouseX, y: mouseY });

            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
    return false; // Evita el desplazamiento de la página
}
```

---

## **📌 2️⃣ `desktop/sketch.js` (Se eliminó `type: 'touch'`)**  
📌 **Ubicación:** `public/desktop/sketch.js`  
📌 **Cambios realizados:**  
✅ **Se eliminó `socket.on('message')`, que esperaba `type: 'touch'`.**  
✅ **Ahora `desktop` solo recibe `posicion_mouse`.**  

🔹 **Código corregido:**  
```js
socket.on("posicion_mouse", (data) => {
    console.log(`📍 Movimiento de ${data.usuario}: X=${data.x}, Y=${data.y}`);
    circleX = data.x;
    circleY = data.y;
});
```

---

## **📌 3️⃣ `server.js` (Se eliminó `socket.on("message")`)**  
📌 **Ubicación:** Raíz del proyecto  
📌 **Cambios realizados:**  
✅ **Se eliminó `socket.on("message")`, que ya no se usaba.**  
✅ **Ahora el servidor solo maneja `posicion_mouse`.**  

🔹 **Código corregido:**  
```js
socket.on("posicion_mouse", (data) => {
    console.log(`📍 ${nombre} movió el mouse a X=${data.x}, Y=${data.y}`);
    io.emit("posicion_mouse", { usuario: nombre, x: data.x, y: data.y });
});
```

---

## **📌 4️⃣ Guardar y reiniciar el servidor**  
1️⃣ **Guarda `mobile/sketch.js`, `desktop/sketch.js` y `server.js`.**  
2️⃣ **Detén el servidor (`Ctrl + C`).**  
3️⃣ **Ejecuta nuevamente:**  
```sh
npm start
```
4️⃣ **Recarga `desktop/index.html` y `mobile/index.html` en el navegador.**  

🚀 **¡Listo! Ahora `type: 'touch'` ya no existe y todo funciona correctamente.** 🎉
