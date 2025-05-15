### **Resumen de WebRTC**

**WebRTC** (Web Real-Time Communication) permite la comunicación en tiempo real (audio, video y datos) entre navegadores sin necesidad de plugins adicionales. Funciona mediante el establecimiento de conexiones directas entre dos dispositivos, conocidos como **peers**, utilizando varios componentes.

### **Componentes clave de WebRTC**:
- **Peer Connection**: Conexión directa entre dos dispositivos para compartir audio, video o datos.
- **Data Channel**: Canal de datos bidireccional entre los peers.
- **Media Stream**: Flujo de medios (audio/video) transmitido entre los peers.
- **ICE Server**: Servidor que ayuda a los peers a conectar a través de NAT/firewalls.
- **STUN Server**: Ayuda a los dispositivos a descubrir su dirección IP pública.
- **TURN Server**: Intermediario que retransmite datos cuando no se puede establecer una conexión directa.
- **Signaling Server**: Facilita el intercambio de información entre peers para establecer la conexión, pero no maneja los datos directamente.

### **Pasos para iniciar WebRTC**:
1. **Configuración del servidor de señalización**: Implementar un servidor (usualmente con WebSocket o HTTP) para intercambiar mensajes entre los peers.
2. **Crear una Peer Connection**: Usar la API WebRTC para establecer una conexión entre los dispositivos.
3. **Configurar STUN/TURN**: Utilizar servidores STUN para determinar la IP pública, y TURN si no se puede conectar directamente.
4. **Intercambiar Media Streams**: Capturar y enviar audio/video mediante las APIs de WebRTC.
5. **Establecer un Data Channel**: Para compartir datos en tiempo real entre los peers.
6. **Negociación y establecimiento de conexión**: Realizar la señalización para coordinar la conexión entre los peers (usando el servidor de señalización).

### **Hallazgos**:
- WebRTC facilita la creación de aplicaciones de comunicación sin necesidad de plugins.
- Requiere de una infraestructura de servidores (STUN, TURN, y señalización).
- Necesita manejar la señalización correctamente para coordinar la conexión.

### **Requisitos iniciales**:
- **Servidor de señalización** (como WebSocket).
- **STUN y TURN servers** para gestionar la conexión entre los peers en diferentes redes.
- Implementar la API WebRTC para establecer conexiones y transmitir datos/media.

En "Frases del Cora", **WebSocket** se utiliza para gestionar la comunicación en tiempo real entre dos usuarios. Cuando un usuario genera una frase, WebSocket envía ese mensaje al otro usuario, quien puede ver y escuchar la frase en tiempo real. Además, WebSocket facilita el intercambio de datos entre los navegadores para crear una conexión WebRTC, permitiendo la grabación y transmisión de audio. El servidor WebSocket retransmite los mensajes de señalización (como la oferta, respuesta y candidatos ICE) necesarios para establecer la conexión, haciendo posible la interacción fluida entre los usuarios.
