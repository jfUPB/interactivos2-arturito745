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


