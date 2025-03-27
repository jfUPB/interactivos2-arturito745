**Propuesta de Aplicación con p5LiveMedia**

### Descripción de la Aplicación
Se propone una pizarra colaborativa en tiempo real que permita a los usuarios dibujar simultáneamente desde diferentes dispositivos conectados. La aplicación soporta conexiones entre usuarios móviles y de escritorio, diferenciándolos con distintos colores. Esto facilitaría la interacción remota en proyectos educativos y creativos.

### Uso de p5LiveMedia
La aplicación utiliza la biblioteca p5LiveMedia para compartir en tiempo real los datos de los trazos de dibujo. Cada usuario envía las coordenadas de sus dibujos al servidor, y este las retransmite a todos los demás participantes conectados, asegurando una experiencia sincronizada.

### Relación con el Proyecto de Curso
Esta aplicación está alineada con la necesidad de mejorar la productividad y la colaboración para personas con TDAH. Permite la organización visual de ideas mediante dibujos y esquemas compartidos en tiempo real, promoviendo un aprendizaje interactivo.

### Tutorial para Replicar la Aplicación
1. **Configurar el servidor**
   - Crear un archivo `server.js` con el siguiente contenido:
   ```js
   const express = require('express');
   const http = require('http');
   const socketIO = require('socket.io');
   const path = require('path');

   const app = express();
   const server = http.createServer(app);
   const io = socketIO(server, {
       cors: {
           origin: "*",
           methods: ["GET", "POST"]
       }
   });

   app.use(express.static(path.join(__dirname, 'public')));

   io.on('connection', (socket) => {
       console.log(`Nuevo cliente conectado: ${socket.id}`);
       socket.on('draw', (data) => {
           socket.broadcast.emit('draw', data);
       });
   });

   const port = process.env.PORT || 3000;
   server.listen(port, '0.0.0.0', () => {
       console.log(`Servidor corriendo en ${process.env.CODESPACE_NAME ? `https://${process.env.CODESPACE_NAME}-3000.github.dev` : `http://localhost:${port}`}`);
   });
   ```

2. **Crear la interfaz en index.html**
   - Crear un archivo `index.html` dentro de la carpeta `public`:
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="utf-8" />
       <title>WebRTC con p5.js</title>
       <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.min.js"></script>
       <script src="/socket.io/socket.io.js"></script>
       <script src="https://p5livemedia.itp.io/p5livemedia.js"></script>
       <script src="https://p5livemedia.itp.io/simplepeer.min.js"></script>
       <script src="https://p5livemedia.itp.io/socket.io.js"></script>
   </head>
   <body>
       <script src="./sketch.js"></script>
   </body>
   </html>
   ```

3. **Implementar la lógica en p5.js**
   - Crear un archivo `sketch.js` en la carpeta `public`. El mismo archivo es utilizado tanto para el cliente de escritorio como para el cliente móvil:
   ```js
   let socket;
   let colorStroke = 'black';
   let userType = null;

   function setup() {
       createCanvas(800, 600);
       background(255);
       socket = io({
           path: "/socket.io",
           transports: ["polling"],
           reconnection: true,
           reconnectionAttempts: 10,
           reconnectionDelay: 1000
       });

       socket.on('draw', (data) => {
           stroke(data.color);
           strokeWeight(5);
           line(data.x1, data.y1, data.x2, data.y2);
       });

       createButton('Soy Desktop').position(10, 10).mousePressed(() => setUserType('desktop'));
       createButton('Soy Mobile').position(120, 10).mousePressed(() => setUserType('mobile'));
   }

   function setUserType(type) {
       userType = type;
       colorStroke = (type === 'mobile') ? 'lime' : 'black';
   }

   function mouseDragged() {
       if (!userType) return;
       let data = { x1: pmouseX, y1: pmouseY, x2: mouseX, y2: mouseY, color: colorStroke };
       stroke(colorStroke);
       strokeWeight(5);
       line(data.x1, data.y1, data.x2, data.y2);
       socket.emit('draw', data);
   }
   ```

4. **Ejecutar el servidor**
   ```sh
   node server.js
   ```
   
5. **Abrir el navegador**
   - Visitar `http://localhost:3000` en distintos dispositivos para probar la pizarra colaborativa.

### Enlaces y Recursos
- [p5.js](https://p5js.org/)
- [p5LiveMedia](https://itpnyu.github.io/p5LiveMedia/)
- [Socket.IO](https://socket.io/)

### Prueba la Pizarra colaborativa 
<a href="https://effective-space-waffle-5gg6g6p94rr7hp76q-3000.app.github.dev/desktop/index.html" target="_blank">Acceder a la aplicación</a>
