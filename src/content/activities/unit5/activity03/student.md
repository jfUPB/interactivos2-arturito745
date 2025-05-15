## Diseño Preliminar de la Experiencia: **Montblanc Sensory - Mirar lo que hueles**

### **1. ¿Qué pasa antes de la experiencia?**
- Los invitados reciben una invitación digital con detalles sobre el evento.
- Se les adelanta que su participación será clave para la activación de la fragancia.
- Al llegar, encuentran un espacio elegante y enigmático con iluminación tenue, efectos de humo y música ambiental envolvente.
- Un artista reconocido inicia su show en vivo sobre una tarima minimalista, preparando el ambiente.
- Dos esculturas monumentales del perfume, rodeadas de un jardín de flores mecánicas cerradas, se presentan como parte del misterio.

### **2. ¿Qué pasa durante la experiencia?**
#### **Inicio de la experiencia**
- Al finalizar su presentación, el artista introduce la experiencia titulada **“Mirada hacia el olfato”**.
- Un difusor tipo humidificador libera la fragancia en el aire, marcando el comienzo de la interacción.
- La pantalla principal muestra una animación con un mensaje en un móvil: **“Mira tu celular”**.
- Cada invitado recibe un enlace en su móvil con el mensaje **“Ingresa aquí”**, llevándolo a una interfaz donde debe elegir las notas olfativas que percibe.

#### **Interacción y progresión**
- Cada invitado selecciona **4 de 8 notas olfativas** (cítricos, flores, vainilla, etc.).
- Al enviar sus elecciones, **una obra de arte generativa** comienza a proyectarse en pantallas, visualizando en tiempo real los inputs enviados.
- Los colores y animaciones reflejan cada nota y se combinan con las de otros participantes para generar una obra única.
- Después de elegir, pueden votar su impresión general del aroma:
  - ❤️ “Me encantó”
  - 👍 “Me gustó”
  - 👎 “No me gustó”
- La pantalla principal muestra el avance colectivo hacia diferentes **checkpoints** que desbloquean cambios en el ambiente:
  - **20%**: Las esculturas comienzan a iluminarse.
  - **50%**: Se enciende el jardín y aparecen efectos de partículas visuales.
  - **70%**: Las flores comienzan a abrirse y se intensifica la fragancia.
  - **100%**: **Clímax**: Las flores se abren completamente y la fragancia envuelve el espacio junto con una explosión de luces y efectos visuales.

### **3. ¿Qué pasa después de la experiencia?**
- Los invitados reciben en su móvil un **porcentaje de acierto**, indicando qué tan cerca estuvieron de descifrar las notas principales de la fragancia.
- En la pantalla principal aparece la frase final: **“Montblanc: el aroma que se ve”**.
- Una ejecutiva de la marca agradece la participación del público y da paso a la continuación de la fiesta.
- Se refuerza la exclusividad del evento con una sesión social donde los asistentes pueden compartir sus impresiones sobre la fragancia.

### **4. ¿Cómo se conecta la narrativa con la experiencia?**
- La historia de la fragancia se entrelaza con la participación activa del público.
- El concepto **“Mirar lo que hueles”** se materializa en la visualización generativa de las notas olfativas elegidas.
- La progresión visual y física de la experiencia (iluminación, apertura de flores, efectos de humo) refuerza la idea de que el aroma toma forma y se revela ante los sentidos.

### **5. ¿Qué tipo de dispositivos vas a utilizar?**
- **Desktop principal**: Recibe y procesa las selecciones y votos del público.
- **Cliente Desktop 1**: Controla la apertura de las flores mecánicas y la iluminación de las esculturas según los checkpoints alcanzados.
- **Cliente Desktop 2**: Desde Codespaces, gestiona los cambios en la pantalla gigante, activando animaciones generativas.
- **Dispositivos móviles**: Los invitados acceden a la interfaz para elegir sus notas olfativas y votar.
- **Difusores de aroma**: Controlados por API para sincronizar la dispersión de la fragancia con los eventos del show.

### **6. ¿Qué tipo de datos vas a capturar?**
- Selección de notas olfativas por cada invitado.
- Votaciones emocionales (❤️, 👍, 👎).
- Cantidad de participantes activos.
- Porcentaje de avance en cada checkpoint.
- Datos de engagement en la plataforma interactiva.

### **7. ¿Cómo se conectan esos datos con el concepto y la narrativa?**
- La visualización en tiempo real de los datos en forma de arte generativo convierte cada elección en una manifestación visual y sensorial.
- La progresión de los checkpoints refuerza la idea de que la fragancia toma vida a través de la participación colectiva.
- El feedback final sobre el acierto en la identificación de notas olfativas cierra el ciclo de aprendizaje e interacción con la fragancia.

### **8. ¿Qué tipo de control remoto vas a utilizar?**
- La interacción es remota a través de los dispositivos móviles de los asistentes.
- Los sistemas de iluminación, las esculturas y los difusores de aroma están sincronizados mediante software.
- El desktop principal coordina en tiempo real la recepción de inputs y la activación de respuestas físicas y visuales.

### **9. ¿Qué tipo de interacción en tiempo real te gustaría tener?**
- **Visual**: La obra de arte generativa se adapta en vivo a los inputs de los asistentes.
- **Sensorial**: La fragancia se intensifica a medida que avanza la experiencia.
- **Física**: Las esculturas y flores mecánicas reaccionan al nivel de interacción.
- **Social**: Los invitados ven reflejada su participación en tiempo real y sienten que contribuyen activamente al evento.

### **10. ¿Qué tipo de contenido en tiempo real te gustaría generar?**
- Una proyección visual evolutiva basada en los inputs de los asistentes.
- Cambios en la iluminación y la ambientación según el avance en los checkpoints.
- Feedback instantáneo sobre las notas seleccionadas y su relación con la fragancia real.
- Estadísticas en vivo sobre la participación y las preferencias olfativas del público.

Aquí tienes las preguntas con sus respuestas:  

### **1. ¿Qué pasa antes de la experiencia?**  
Los invitados reciben una invitación exclusiva con un código QR para acceder al evento. Al llegar, se les da la bienvenida en un ambiente elegante con luces tenues y música envolvente. La expectativa se construye con un escenario minimalista donde el artista se prepara para su show.  

### **2. ¿Qué pasa durante la experiencia?**  
El artista inicia su presentación y, al finalizar, da inicio a "Mirada hacia el olfato". Un difusor libera la fragancia mientras en la pantalla aparece un mensaje invitando a los asistentes a interactuar. Desde sus móviles, eligen 4 de 8 notas olfativas, lo que activa la generación de arte en tiempo real, impactando la iluminación y el ambiente visual. Los asistentes también votan por su percepción del aroma, desbloqueando fases interactivas.  

### **3. ¿Qué pasa después de la experiencia?**  
El evento cierra con la frase "Montblanc, el aroma que se ve" en la pantalla. Una ejecutiva de la marca agradece a los asistentes y la fiesta continúa con música en vivo. Cada invitado recibe en su móvil un resumen de su interacción, mostrando su porcentaje de coincidencia con la fórmula de la fragancia.  

### **4. ¿Cómo se conecta la narrativa con la experiencia?**  
La experiencia traduce el concepto "Mirar lo que hueles" en una interacción multisensorial, donde el público moldea la obra visual y física a través de sus percepciones olfativas. Todo el proceso refleja la conexión entre fragancia, arte y tecnología.  

### **5. ¿Qué tipo de dispositivos vas a utilizar?**  
- **Desktop principal**: Recibe y procesa los datos de las selecciones y votaciones.  
- **Cliente Desktop 1**: Controla la iluminación y apertura de flores.  
- **Cliente Desktop 2**: Gestiona la animación en la pantalla gigante.  
- **Dispositivos móviles**: Permiten la selección de notas y la votación del público.  

### **6. ¿Qué tipo de datos vas a capturar?**  
- Notas olfativas seleccionadas por cada usuario.  
- Votaciones sobre la fragancia.  
- Cantidad de participantes activos.  
- Checkpoints alcanzados en la experiencia.  

### **7. ¿Cómo se conectan esos datos con el concepto y la narrativa?**  
Los datos permiten transformar la experiencia en tiempo real. Las selecciones individuales generan una obra de arte generativo en pantalla, mientras las votaciones influyen en el desarrollo de la iluminación, la apertura de flores y la difusión de aromas.  

### **8. ¿Qué tipo de control remoto vas a utilizar?**  
Los dispositivos desktop estarán conectados mediante un sistema de comunicación en red, permitiendo que los cambios en las pantallas y las esculturas se activen en función de las interacciones del público.  

### **9. ¿Qué tipo de interacción en tiempo real te gustaría tener?**  
El público verá cómo sus elecciones influyen en el ambiente al instante. La fusión de colores y animaciones en pantalla reflejará la combinación de notas seleccionadas, mientras que la iluminación y los efectos físicos evolucionarán con los votos.  

### **10. ¿Qué tipo de contenido en tiempo real te gustaría generar?**  
- Visualizaciones generativas basadas en las elecciones del público.  
- Cambios en la iluminación y apertura de flores según los checkpoints alcanzados.  
- Feedback final con el porcentaje de acierto en la identificación de la fragancia.  

### **11. ¿Cómo se puede hacer que la experiencia sea más inclusiva?**  
- Ofrecer opciones de accesibilidad en la interfaz móvil.  
- Incluir descripciones sensoriales en audio para personas con discapacidad visual.  
- Asegurar que los dispositivos sean de fácil acceso y uso para todo el público.  

### **12. ¿Qué desafíos técnicos podrían surgir y cómo se pueden solucionar?**  
- **Latencia en la actualización de datos** → Usar comunicación en tiempo real optimizada con WebSockets.  
- **Fallas en la conexión de los dispositivos** → Implementar redundancia con servidores locales.  
- **Dificultad para que todos los asistentes interactúen** → Incluir guías visuales claras en las pantallas y asistentes capacitados para ayudar.  

### **13. ¿Cómo podemos mantener el interés del público incluso después del evento?**  
- Enviar un resumen personalizado con su porcentaje de coincidencia.  
- Ofrecer contenido exclusivo sobre la fragancia en redes sociales.  
- Crear una activación digital donde los participantes puedan compartir su experiencia.  

### **14. ¿Cómo aseguramos que el sistema funcione sin interrupciones?**  
- Realizar pruebas previas con distintos niveles de carga.  
- Contar con un plan de contingencia para fallos técnicos.  
- Tener un equipo de soporte técnico en sitio para resolver cualquier problema al instante.  

### **15. ¿Cómo aseguramos que la experiencia se perciba como un evento exclusivo?**  
- Acceso solo con invitación personalizada.  
- Uso de un ambiente elegante y sofisticado.  
- Integración de tecnología de vanguardia para una experiencia única.  

**Conclusión:**
Esta experiencia convierte el lanzamiento de la fragancia en un evento inmersivo y participativo. Cada asistente se vuelve parte del proceso creativo, viendo y sintiendo cómo su percepción del aroma influye en el espacio. Con tecnología, arte y narrativa entrelazados, **Montblanc Sensory: Mirar lo que hueles** redefine cómo vivimos una fragancia.

