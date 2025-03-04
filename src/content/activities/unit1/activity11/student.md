#####

# Generación de texto aleatorio

```
// Lista de sujetos, verbos y objetos
let subjects = ["El sol", "La luna", "La estrella", "El cielo", "El mar"];
let verbs = ["brilla", "despierta", "cubre", "ilumina", "adormece"];
let objects = ["el horizonte", "la noche", "el día", "la tierra", "el sueño"];

function setup() {
  createCanvas(800, 600); // Crear el lienzo
  background(0); // Fondo negro
  fill(255); // Color blanco para el texto

  // Generar y mostrar una frase coherente
  let phrase = generateRandomSentence();
  textSize(32); // Tamaño del texto
  text(phrase, 100, 300); // Mostrar la frase en la pantalla
}

function generateRandomSentence() {
  // Elegir una palabra aleatoria de cada categoría (sujeto, verbo, objeto)
  let subject = random(subjects);
  let verb = random(verbs);
  let object = random(objects);
  
  // Combinar las palabras en una oración coherente
  return subject + " " + verb + " " + object + ".";
}


```

[Texto del enlace](https://editor.p5js.org/arturito745/sketches/3hCSPonSO)

![imagen](https://github.com/user-attachments/assets/0c7c0423-c119-4198-a1f3-a2e34f70b0f5)
