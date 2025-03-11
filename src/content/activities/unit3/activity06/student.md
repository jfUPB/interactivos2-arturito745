#####

## **📡 Aplicación de Envío de Imágenes y Coordenadas (Mobile → Desktop)**  

Esta aplicación permite enviar imágenes y coordenadas desde un dispositivo **móvil** a un **desktop** mediante **Socket.IO** en tiempo real.  

---

## **📌 Cambios y Mejoras en el Código**  

Durante la evolución de la aplicación, hicimos varias mejoras clave:  

✅ **Corrección de conexión WebSocket** en mobile y desktop para evitar errores.  
✅ **Optimización del envío de coordenadas** con un **umbral de movimiento** en `touchMoved()`.  
✅ **Añadimos la función `subirImagen()`** en el móvil para permitir el envío de imágenes al servidor.  
✅ **Guardamos la última imagen enviada** en el servidor para que los nuevos clientes la reciban al conectarse.  
✅ **Añadimos la función `recibir_imagen`** en desktop para mostrar imágenes enviadas desde el móvil.  
✅ **Modificamos `index.html` en desktop y mobile** para incluir elementos que permiten **enviar y mostrar imágenes**.  

---

## **📜 Código del Servidor (`server.js`)**  

```javascript
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const cors = require('cors');

const app = express();
app.use(cors());
const server = http.createServer(app);
const io = socketIO(server, { cors: { origin: "*", methods: ["GET", "POST"] } });

const port = 3000;
app.use(express.static('public'));
let ultimaImagen = null; // 🔹 Guarda la última imagen enviada

io.on('connection', (socket) => {
    let nombre = `Cliente-${Math.floor(Math.random() * 1000)}`;
    console.log(`🟢 ${nombre} conectado`);

    if (ultimaImagen) socket.emit("recibir_imagen", ultimaImagen); // Enviar la última imagen si existe
    
    socket.on("posicion_mouse", (data) => io.emit("posicion_mouse", { usuario: nombre, x: data.x, y: data.y }));
    
    socket.on("enviar_imagen", (data) => {
        console.log(`📸 Imagen recibida de ${nombre}`);
        ultimaImagen = data; // Guardar la última imagen
        io.emit("recibir_imagen", data); // Enviar la imagen a todos
    });

    socket.on('disconnect', () => console.log(`🔴 ${nombre} desconectado`));
});

server.listen(port, () => console.log(`🚀 Servidor en http://localhost:${port}`));
```

---

## **📜 Código del Cliente Desktop (`index.html` y `sketch.js`)**  

### **📄 `index.html` (Desktop)**
```html
<body>
    <img id="imagenRecibida" style="max-width: 100%; display: none;"> <!-- Imagen recibida desde el móvil -->
</body>
```

### **📄 `sketch.js` (Desktop)**
```javascript
let socket, circleX = 200, circleY = 200;
function setup() {
    createCanvas(400, 400);
    socket = io("http://localhost:3000");

    socket.on("posicion_mouse", (data) => { circleX = data.x; circleY = data.y; });

    socket.on("recibir_imagen", (data) => { 
        console.log("📸 Imagen recibida");
        let imgElement = document.getElementById("imagenRecibida");
        imgElement.src = data; 
        imgElement.style.display = "block"; 
    });
}

function draw() {
    background(220); fill(255, 0, 0);
    ellipse(circleX, circleY, 50, 50);
}
```

🔹 **Nuevo `<img>` en `index.html` para mostrar imágenes enviadas desde el móvil.**  
🔹 **Función `recibir_imagen` en `sketch.js` para actualizar la imagen cuando el servidor la envía.**  

---

## **📜 Código del Cliente Mobile (`index.html` y `sketch.js`)**  

### **📄 `index.html` (Mobile)**
```html
<body>
    <label for="cameraInput">Selecciona una imagen:</label>
    <input type="file" accept="image/*" capture="environment" id="cameraInput">
    <button onclick="subirImagen()">Enviar Imagen</button>    
</body>
```

### **📄 `sketch.js` (Mobile)**
```javascript
let socket = io("http://localhost:3000"), lastTouchX, lastTouchY, threshold = 5;
function setup() { createCanvas(400, 400); }
function draw() { background(220); text("Touch to move", width / 2, height / 2); }
function touchMoved() {
    if (socket.connected && (abs(mouseX - lastTouchX) > threshold || abs(mouseY - lastTouchY) > threshold)) {
        socket.emit("posicion_mouse", { x: mouseX, y: mouseY });
        lastTouchX = mouseX; lastTouchY = mouseY;
    }
    return false;
}
function subirImagen() {
    const input = document.getElementById("cameraInput");
    if (input.files.length > 0) {
        const reader = new FileReader();
        reader.onload = (event) => socket.emit("enviar_imagen", event.target.result);
        reader.readAsDataURL(input.files[0]);
        console.log("📤 Imagen enviada al servidor");
    }
}
```

🔹 **Añadimos un `<input>` y un `<button>` en `index.html` para seleccionar y enviar imágenes.**  
🔹 **Nueva función `subirImagen()` en `sketch.js` para convertir la imagen a base64 y enviarla al servidor.**  
🔹 **Corrección en `touchMoved()` para evitar enviar coordenadas constantemente.**  

---

## **🛠️ Explicación del Funcionamiento**
### **📡 ¿Cómo se comunican los clientes con el servidor?**  
✅ **WebSockets con `Socket.IO`**.  
✅ **El móvil envía coordenadas e imágenes al servidor.**  
✅ **El servidor retransmite estos datos a los clientes de escritorio.**  

### **🔄 ¿Cómo se comunican los clientes entre sí?**  
Los clientes **no se comunican directamente**, el servidor actúa como intermediario.  

### **📩 ¿Qué tipo de mensajes se envían?**  
- **`posicion_mouse`** → Coordenadas del cursor.  
- **`enviar_imagen`** → Imágenes enviadas desde el móvil.  
- **`recibir_imagen`** → Imagen reenviada por el servidor a los clientes.  

### **📂 ¿Qué tipo de datos se envían?**  
- **JSON** `{x, y}` para coordenadas.  
- **Base64** para imágenes.  

### **📍 ¿Qué tipo de eventos se generan?**  
- **`connection`** → Cliente nuevo se conecta.  
- **`posicion_mouse`** → Movimiento del cursor.  
- **`enviar_imagen`** → El móvil envía imágenes.  
- **`recibir_imagen`** → El desktop recibe imágenes.  
- **`disconnect`** → Cliente se desconecta.  

---

## **🔄 Flujo de Datos**
### **📲 Móvil → Servidor → Desktop**
1. **El móvil toca la pantalla** → Envía coordenadas (`posicion_mouse`).  
2. **El servidor retransmite** la posición.  
3. **El Desktop actualiza el círculo en pantalla.**  

### **📷 Móvil → Servidor → Desktop**
1. **El móvil selecciona una imagen** y la envía (`enviar_imagen`).  
2. **El servidor la almacena** y la reenvía (`recibir_imagen`).  
3. **El Desktop la muestra en pantalla.**  

---

## **🎯 Conclusión**
Hemos construido una aplicación funcional que permite **enviar imágenes y coordenadas** desde un **móvil** a un **desktop** en tiempo real. 🚀  

✅ **WebSockets optimizados** para evitar errores y mejorar rendimiento.  
✅ **Interfaz mejorada** para subir y visualizar imágenes.  
✅ **Servidor eficiente** con almacenamiento de última imagen.  

💡 **Posibles mejoras:**  
- **Autenticación de usuarios** para mayor seguridad.  
- **Compresión de imágenes** para optimizar la transferencia.  
- **Interfaz más atractiva** con feedback visual en desktop y mobile.  

🔥 **Aplicación lista y funcional!** 🚀 ¿Necesitas más mejoras? 😃
