#####
# Creación de un patrón generativo simple

Ejemplo: [EJM](http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_1_5_02)


```
let circleX, circleY, mainCircleRadius, clickCircleRadius;
let clickCircles = []; // Array para almacenar los círculos generados por clics

function setup() {
  createCanvas(800, 800);
  background(0); // Fondo negro
  circleX = width / 2;
  circleY = height / 2;
  mainCircleRadius = 120; // Radio del círculo blanco
  clickCircleRadius = 30; // Radio de los círculos generados al hacer clic
  noStroke(); // Sin contorno para los círculos generados
}

function draw() {
  background(0); // Redibujar el fondo negro en cada fotograma

  // Dibujar el círculo blanco en el centro
  fill(255); 
  ellipse(circleX, circleY, mainCircleRadius * 2, mainCircleRadius * 2);

  // Dibujar todos los círculos generados por clics
  for (let i = 0; i < clickCircles.length; i++) {
    let c = clickCircles[i];
    fill(200); // Gris claro para los círculos generados
    ellipse(c.x, c.y, clickCircleRadius * 2, clickCircleRadius * 2); // Dibujar los círculos pequeños
  }
}

function mousePressed() {
  // Al hacer clic, agregar un nuevo círculo a la lista
  clickCircles.push(createVector(mouseX, mouseY)); // Guardar la posición del clic
}


```
[Reconstruccion](https://editor.p5js.org/arturito745/sketches/3hCSPonSO)
