
### **Descripción de la Aplicación Propuesta**

**Nombre del Proyecto**: **Frases del Cora**

La aplicación permitirá que los usuarios elijan palabras o frases predeterminadas (como "amor", "comprensión", "respeto", etc.), las organicen en una frase personalizada, y luego puedan escuchar la frase leída en voz alta por el navegador. El sistema también presentará la frase en la pantalla con efectos visuales sencillos y, en el futuro, podrá enviar esta creación por correo electrónico.

---

### **Cómo hace uso de p5LiveMedia**

Aunque **p5LiveMedia** es principalmente una biblioteca para interactuar con audio y video en tiempo real, en este caso la utilizaremos en conjunto con **p5.js** para crear una interfaz interactiva. Utilizaremos **p5LiveMedia** para gestionar la entrada de audio y visualizar el contenido multimedia en la pantalla, como los efectos visuales que acompañan la frase generada.

En esta fase inicial del proyecto, la interacción con el audio será principalmente para **leer la frase en voz alta** usando la API de **SpeechSynthesis** (nativa de JavaScript), lo que puede ser considerado un "audio en tiempo real" desde la perspectiva del usuario.

---

### **Relación con el Proyecto de Curso**

Este proyecto se alinea perfectamente con el concepto de **interactividad** en tiempo real y **creación de obras multimedia**. Los estudiantes podrán:

1. Crear una interfaz donde las palabras se seleccionan en tiempo real.
2. Manipular audio en tiempo real (con el uso de SpeechSynthesis para lectura en voz alta).
3. Crear efectos visuales interactivos, lo que es una aplicación directa de los conceptos de interacción con medios en vivo.
4. La escalabilidad del proyecto permitirá agregar características adicionales (como el envío de correos electrónicos) a medida que el curso avance.

---

### **Tutorial para Replicar la Aplicación**

#### **1. Instalación de p5.js**

1. Ve a [p5.js](https://p5js.org/download/) y descarga el editor o usa la versión online en [p5.js Web Editor](https://editor.p5js.org/).
2. Si prefieres trabajar en tu propio entorno, crea una carpeta para tu proyecto y descarga **p5.js** desde su [repositorio](https://github.com/processing/p5.js).

---

#### **2. Crear la Interfaz y Funcionalidad Básica**

**Estructura del Proyecto:**
- `index.html`: Para la estructura básica de la aplicación.
- `sketch.js`: Contendrá el código de la aplicación p5.js.

##### **index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Frases del Corazón</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
  <script src="sketch.js"></script>
</head>
<body>
  <h1>Frases del Corazón</h1>
  <p>Selecciona algunas palabras para crear tu mensaje personal</p>
  <div id="word-list"></div>
</body>
</html>
```

##### **sketch.js**

```javascript
let words = ["amor", "comprensión", "respeto", "te quiero", "te adoro", "contigo me imagino", "te estimo", "estoy orgulloso"];
let selectedWords = [];
let userPhrase = "";
let synth;

function setup() {
  createCanvas(600, 400);
  synth = window.speechSynthesis;  // Inicializar SpeechSynthesis

  let yPos = 100;
  for (let i = 0; i < words.length; i++) {
    let wordButton = createButton(words[i]);
    wordButton.position(50, yPos);
    wordButton.mousePressed(() => addWord(words[i])); // Al hacer clic en la palabra, la agregamos
    yPos += 40;
  }

  // Botón para generar la frase
  let generateButton = createButton("Generar Frase");
  generateButton.position(50, yPos);
  generateButton.mousePressed(generatePhrase);

  // Botón para leer la frase en voz alta
  let readButton = createButton("Leer en voz alta");
  readButton.position(200, yPos);
  readButton.mousePressed(speakPhrase);
}

function addWord(word) {
  selectedWords.push(word);
  userPhrase = selectedWords.join(' ');
  console.log(userPhrase); // Muestra la frase en consola
}

function generatePhrase() {
  background(220);
  textSize(24);
  textAlign(CENTER);
  text(userPhrase, width / 2, height / 2);  // Mostrar la frase generada

  // Generar efectos visuales mientras se muestra la frase
  generateVisualArt(userPhrase);
}

function generateVisualArt(phrase) {
  background(220);
  let wordsArray = phrase.split(" ");
  for (let i = 0; i < wordsArray.length; i++) {
    fill(random(255), random(255), random(255)); // Colores aleatorios
    textSize(30);
    text(wordsArray[i], random(width), random(height)); // Palabras flotando
  }
}

function speakPhrase() {
  let utterThis = new SpeechSynthesisUtterance(userPhrase);
  synth.speak(utterThis); // Reproduce la frase en voz alta
  utterThis.onend = function() {
    console.log("La frase fue leída.");
  }
}
```

---

### **3. Explicación del Código**

1. **Interfaz de Usuario**:
   - Creamos botones para cada palabra que el usuario puede seleccionar. Cuando se hace clic en una palabra, se agrega a la lista `selectedWords`.
   
2. **Generar la Frase**:
   - Al presionar el botón "Generar Frase", se concatenan las palabras seleccionadas y se muestran en la pantalla.
   
3. **Lectura de la Frase**:
   - La API de **SpeechSynthesis** permite leer en voz alta la frase generada.
   
4. **Efectos Visuales**:
   - Se generan efectos visuales sencillos donde las palabras se desplazan y cambian de color en función de la frase generada.

---

### **4. Escalabilidad del Proyecto**

Este proyecto es solo la base, y puedes escalarlo de muchas formas. Algunas ideas para expandirlo:

1. **Añadir más interacción**:
   - Permitir que los usuarios escriban sus propias palabras en lugar de elegir solo de una lista predeterminada.
   - Implementar más efectos visuales y sonoros que reaccionen en tiempo real a las palabras.

2. **Guardar y Enviar por Correo**:
   - Implementar una funcionalidad que permita guardar la obra de arte (imagen + audio) como archivo.
   - Utilizar servicios como **EmailJS** o crear un backend sencillo para enviar el correo con los archivos adjuntos.

3. **Más Personalización**:
   - Permitir que los usuarios personalicen el fondo, la tipografía y el estilo de los efectos visuales.
   - Ofrecer una opción para elegir voces diferentes para la lectura de la frase.

---

### **5. Recursos Adicionales y Enlaces**

- [Documentación de p5.js](https://p5js.org/reference/)
- [SpeechSynthesis API](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis)
- [EmailJS (enviar correo desde navegador)](https://www.emailjs.com/)

---


