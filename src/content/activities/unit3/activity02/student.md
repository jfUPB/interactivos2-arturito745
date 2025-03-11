**Documentación de Ejecución de la Aplicación**

### Introducción
Esta documentación detalla los pasos seguidos para ejecutar la aplicación basada en **Node.js** y **Socket.IO**, alojada en un repositorio de **GitHub** y ejecutada en **CodeSpaces**.

---

### **1. Fork del Repositorio**
- Se realiza un **fork** del repositorio original `juanferfranco/sfiSocketioDesktopMobile` hacia `juanferfrancoudea/sfiSocketioDesktopMobile`.
- Esto permite trabajar en una copia independiente del código fuente.

### **2. Creación de un CodeSpace**
- Se accede a GitHub y desde el repositorio forkeado se inicia un **GitHub CodeSpace**.
- Esto genera un entorno de desarrollo basado en la nube con todas las dependencias necesarias.

### **3. Clonación del Repositorio en CodeSpaces**
- Dentro de CodeSpaces, se ejecuta:
  ```sh
  git clone https://github.com/juanferfrancoudea/sfiSocketioDesktopMobile.git
  ```
- Esto crea una copia local del repositorio en el entorno de desarrollo.

### **4. Instalación de Dependencias**
- Se navega al directorio del proyecto:
  ```sh
  cd sfiSocketioDesktopMobile
  ```
- Se instalan las dependencias de **Node.js** especificadas en `package.json`:
  ```sh
  npm install
  ```

### **5. Ejecución del Servidor**
- Se inicia el servidor con el siguiente comando:
  ```sh
  node server.js
  ```
- Esto levanta el servidor en el puerto **3000**, permitiendo la conexión con clientes mediante HTTP y WebSockets.

### **6. Conexión de Clientes (Web y Móvil)**
- Los clientes acceden a la página web a través de un navegador usando HTTPS.
- **Socket.IO** maneja la comunicación en tiempo real entre el servidor y los clientes.
- Se establecen conexiones **WebSocket (WS)** para enviar y recibir datos en tiempo real.

### **7. Pruebas y Depuración**
- Se verifican las conexiones con mensajes de prueba en la consola.
- Se monitorean errores en el servidor y en los clientes.
- Se realizan pruebas de comunicación bidireccional con **Socket.IO**.

---

### **Conclusión**
Siguiendo estos pasos, la aplicación se ejecuta correctamente en un entorno de desarrollo basado en **GitHub CodeSpaces**, permitiendo interacciones en tiempo real entre los clientes y el servidor.

