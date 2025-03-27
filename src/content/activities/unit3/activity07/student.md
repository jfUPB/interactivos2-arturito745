#####


## **Conceptos aprendidos en cada actividad de la unidad**  

### **1. Fundamentos de Comunicación en Tiempo Real**  
- **Sockets** → Son canales de comunicación en tiempo real que permiten que los clientes y el servidor intercambien información sin necesidad de recargar la página.  
- **Eventos en `socket.io`** → Se usan para enviar y recibir mensajes entre los clientes y el servidor.  

### **2. Configuración del Servidor con `express` y `socket.io`**  
- **`Express.js`** → Framework para crear servidores en Node.js. Se usó para manejar las peticiones y servir archivos estáticos.  
- **`socket.io` en el servidor** → Permite establecer una conexión entre múltiples clientes y manejar eventos personalizados.  

### **3. Implementación del Cliente (Mobile y Desktop)**  
- **Diferencias entre cliente móvil y de escritorio** → Un cliente captura la imagen (móvil) y otro la recibe (escritorio).  
- **`input type="file"` con `capture="environment"`** → Permite que la cámara se use automáticamente en dispositivos móviles.  
- **Conversión de imágenes a base64** → Necesario para enviar imágenes como texto a través de `socket.io`.  

### **4. Manejo de eventos en `socket.io`**  
- **Eventos personalizados** → `enviar_imagen` y `recibir_imagen` se usaron para transmitir imágenes entre clientes.  
- **`emit` y `on` en `socket.io`** → Se usaron para enviar y recibir datos en tiempo real.  

---

## **Conceptos nuevos aprendidos**  
- Cómo transmitir imágenes en tiempo real usando `socket.io`.  
- Conversión de imágenes a base64 para transmisión.  
- Manejo de eventos en `socket.io` y su uso para diferentes clientes.  

---

## **Conceptos más difíciles de entender**  
- **Conversión y manejo de imágenes en base64** → No es intuitivo convertir imágenes en base64 y luego enviarlas.  
- **Gestión de eventos en `socket.io`** → Al principio fue difícil organizar qué eventos manejar en el móvil y en el escritorio.  

---

## **Análisis de la Aplicación (Actividad 6)**  
Aquí está la estructura de la aplicación y cómo aplicamos los conceptos aprendidos.  

### **1. Servidor (`server.js`)**  
**Uso de `express` y `socket.io`**  
```javascript
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const cors = require('cors');

const app = express();
app.use(cors());

const server = http.createServer(app); 
const io = socketIO(server, {
    cors: { origin: "*", methods: ["GET", "POST"] }
});
```
**Manejo de conexiones de clientes**  
```javascript
io.on('connection', (socket) => {
    console.log(`Cliente conectado`);
    
    socket.on("enviar_imagen", (data) => {
        console.log(`Imagen recibida`);
        io.emit("recibir_imagen", data); // Reenvía la imagen a todos los clientes
    });
});
```

### **2. Cliente Mobile (`index.html` y `sketch.js`)**  
**Captura de imagen desde el móvil**  
```html
<label for="cameraInput">Selecciona una imagen:</label>
<input type="file" accept="image/*" capture="environment" id="cameraInput">
<button onclick="subirImagen()">Enviar Imagen</button>
```
**Conversión de imagen a base64 y envío al servidor**  
```javascript
function subirImagen() {
    let input = document.getElementById("cameraInput");
    let file = input.files[0];

    if (file) {
        let reader = new FileReader();
        reader.onload = function (event) {
            let imageData = event.target.result;
            socket.emit("enviar_imagen", imageData);
        };
        reader.readAsDataURL(file);
    }
}
```

### **3. Cliente Desktop (`sketch.js`)**  
**Recepción y visualización de la imagen**  
```javascript
socket.on("recibir_imagen", (data) => {
    let img = new Image();
    img.src = data;
    img.onload = function () {
        let canvas = document.createElement("canvas");
        let ctx = canvas.getContext("2d");
        canvas.width = img.width;
        canvas.height = img.height;
        ctx.drawImage(img, 0, 0);
        document.body.appendChild(canvas);
    };
});
```

---

## **Limitaciones del modelo input-procesamiento-output en esta unidad**  
- **No hay procesamiento avanzado de la imagen** → Solo se transmite la imagen, pero no se hace edición ni filtrado.  
- **No hay almacenamiento de imágenes en el servidor** → Si se recarga la página, la imagen desaparece.  
- **No hay autenticación o permisos para los clientes** → Cualquiera puede enviar imágenes sin restricciones.  

---

## **¿Qué aprender para superar estas limitaciones?**  
- **Almacenamiento de imágenes en el servidor** (usando `multer` o Firebase Storage).  
- **Procesamiento de imágenes** (usando `Canvas API` o `TensorFlow.js` para manipulación).  
- **Autenticación de usuarios** para restringir el acceso (con Firebase Auth o JWT).  

---

## **Conclusión**  
Esta unidad nos permitió construir una aplicación funcional con `socket.io`, aprendimos a manejar eventos en tiempo real y logramos enviar imágenes entre clientes. Sin embargo, para hacer una experiencia más robusta, necesitamos mejorar el almacenamiento, la seguridad y el procesamiento de imágenes.
