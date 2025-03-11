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
###  (Reciben y muestran en consola)**  
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


