#####
# Manipulación de imágenes con código

### Codigo 

```
let img;
let originalImg; // Imagen original para restaurar colores
let colorModeIndex = 0; // Controla la secuencia de colores

function preload() {
  originalImg = loadImage('https://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Cat03.jpg/800px-Cat03.jpg'); // Cargar imagen fija
}

function setup() {
  createCanvas(900, 900);
  img = createImage(originalImg.width, originalImg.height);
  img.copy(originalImg, 0, 0, originalImg.width, originalImg.height, 0, 0, img.width, img.height); // Copiar la imagen original
  noLoop(); // Evita que draw() se ejecute en bucle
}

function draw() {
  img.loadPixels();

  for (let y = 0; y < img.height; y++) {
    for (let x = 0; x < img.width; x++) {
      let index = (x + y * img.width) * 4; // Posición en el array de píxeles

      let r = img.pixels[index + 0]; // Rojo
      let g = img.pixels[index + 1]; // Verde
      let b = img.pixels[index + 2]; // Azul

      // Cambio cíclico de colores asegurando que la imagen no se pierda
      switch (colorModeIndex) {
        case 0: // Morado (Rojo + Azul)
          img.pixels[index + 0] = r;
          img.pixels[index + 1] = g * 0.3;
          img.pixels[index + 2] = b;
          break;
        case 1: // Magenta
          img.pixels[index + 0] = r;
          img.pixels[index + 1] = g * 0.2;
          img.pixels[index + 2] = 150 + b * 0.5;
          break;
        case 2: // Amarillo
          img.pixels[index + 0] = r;
          img.pixels[index + 1] = g;
          img.pixels[index + 2] = b * 0.3;
          break;
        case 3: // Verde fuerte
          img.pixels[index + 0] = r * 0.3;
          img.pixels[index + 1] = g;
          img.pixels[index + 2] = b * 0.3;
          break;
        case 4: // Azul fuerte
          img.pixels[index + 0] = r * 0.3;
          img.pixels[index + 1] = g * 0.3;
          img.pixels[index + 2] = b;
          break;
      }
    }
  }

  img.updatePixels();
  image(img, 0, 0);
}

// Cambia los colores en ciclo cada vez que se haga clic
function mousePressed() {
  colorModeIndex = (colorModeIndex + 1) % 5; // Mantiene el ciclo de 5 colores
  img.copy(originalImg, 0, 0, originalImg.width, originalImg.height, 0, 0, img.width, img.height); // Restaurar la imagen original
  redraw(); // Llama a draw() de nuevo para actualizar la imagen
}

```
![image](https://github.com/user-attachments/assets/495eda25-e0a2-4ef5-9121-522982c67f60)
