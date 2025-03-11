##### 
# Generación de formas geométricas aleatorias

Codigo:

```
let lastTime = 0; // Variable para almacenar el tiempo de la última vez que se dibujó una forma

function setup() {
  createCanvas(600, 600); // Crear el lienzo con un tamaño de 600x600 píxeles
  noStroke(); // Desactivar el contorno de las formas
  frameRate(30); // Reducir la velocidad de fotogramas para hacer la animación más lenta
  background(0); // Fondo negro
}

function draw() {
  // Generar nuevas formas cada 500 milisegundos (0.5 segundos)
  if (millis() - lastTime > 500) {
    lastTime = millis(); // Actualizar el tiempo de la última forma generada

    let shapeType = int(random(3)); // 0 = círculo, 1 = cuadrado, 2 = triángulo
    
    let x = random(width); // Posición aleatoria en el eje X
    let y = random(height); // Posición aleatoria en el eje Y
    let size = random(20, 150); // Tamaño aleatorio entre 20 y 150 píxeles
    let color1 = random(255); // Color aleatorio para el rojo
    let color2 = random(255); // Color aleatorio para el verde
    let color3 = random(255); // Color aleatorio para el azul

    // Aplicar el color aleatorio
    fill(color1, color2, color3);

    // Dibuja el tipo de forma correspondiente
    if (shapeType == 0) {
      ellipse(x, y, size, size); // Dibuja un círculo
    } else if (shapeType == 1) {
      rect(x, y, size, size); // Dibuja un cuadrado
    } else if (shapeType == 2) {
      triangle(x, y, x + size, y, x + size / 2, y - size); // Dibuja un triángulo
    }
  }
}


```
View

![imagen](https://github.com/user-attachments/assets/d8e8b7ed-3a27-4694-afca-3a305ccb89b8)
