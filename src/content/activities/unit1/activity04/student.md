##### 
# Exploración de código generativo
link: https://p5js.org/examples/3d-orbit-control/

#### CODIGO 

```
function setup() {
  createCanvas(710, 400, WEBGL);
  angleMode(DEGREES);
  strokeWeight(5);
  noFill();
  stroke(32, 8, 64);
  describe(
    'Users can click on the screen and drag to adjust their perspective in 3D space. The space contains a sphere of dark purple cubes on a light pink background.'
  );
}

function draw() {
  background(250, 180, 200);

  // Call every frame to adjust camera based on mouse/touch
  orbitControl();

  // Rotate rings in a half circle to create a sphere of cubes
  for (let zAngle = 0; zAngle < 180; zAngle += 30) {
    // Rotate cubes in a full circle to create a ring of cubes
    for (let xAngle = 0; xAngle < 360; xAngle += 30) {
      push();

      // Rotate from center of sphere
      rotateZ(zAngle);
      rotateX(xAngle);

      // Then translate down 400 units
      translate(0, 400, 0);
      box();
      pop();
    }
  }
}
```
#### Descripcion 



```
function setup() {
  // Crea un lienzo de 710x400 píxeles en 3D con WEBGL
  createCanvas(710, 400, WEBGL);
  
  // Configura el modo de ángulos en grados (en lugar de radianes)
  angleMode(DEGREES);
  
  // Establece el grosor de las líneas en 5 píxeles
  strokeWeight(5);
  
  // Define el color del borde de los cubos (púrpura oscuro)
  stroke(32, 8, 64);
  
  // Proporciona una descripción de lo que hace el código
  describe('Puedes hacer clic y arrastrar para ajustar la vista 3D. Hay una esfera formada por cubos púrpuras sobre un fondo rosa.');
}

function draw() {
  // Establece un fondo de color rosa claro
  background(250, 180, 200);

  // Permite que el usuario mueva la cámara con el ratón (o la pantalla táctil)
  orbitControl();

  // Crea los cubos en una esfera, con dos bucles
  for (let zAngle = 0; zAngle < 180; zAngle += 30) { // Rotación alrededor del eje Z
    for (let xAngle = 0; xAngle < 360; xAngle += 30) { // Rotación alrededor del eje X
      push(); // Guarda el estado actual de transformaciones

      // Rota el cubo alrededor de los ejes Z y X
      rotateZ(zAngle);
      rotateX(xAngle);

      // Mueve los cubos lejos del centro (400 unidades en el eje Y)
      translate(0, 400, 0);

      // Dibuja un cubo
      box();

      pop(); // Restaura el estado de transformaciones anterior
    }
  }
}
```

### Resumen de lo que hace el código:

```
function setup() {
  // Crea un lienzo de 710x400 píxeles en 3D con WEBGL
  createCanvas(710, 400, WEBGL);
  
  // Configura el modo de ángulos en grados (en lugar de radianes)
  angleMode(DEGREES);
  
  // Establece el grosor de las líneas en 5 píxeles
  strokeWeight(5);
  
  // Define el color del borde de los cubos (púrpura oscuro)
  stroke(32, 8, 64);
  
  // Proporciona una descripción de lo que hace el código
  describe('Puedes hacer clic y arrastrar para ajustar la vista 3D. Hay una esfera formada por cubos púrpuras sobre un fondo rosa.');
}

function draw() {
  // Establece un fondo de color rosa claro
  background(250, 180, 200);

  // Permite que el usuario mueva la cámara con el ratón (o la pantalla táctil)
  orbitControl();

  // Crea los cubos en una esfera, con dos bucles
  for (let zAngle = 0; zAngle < 180; zAngle += 30) { // Rotación alrededor del eje Z
    for (let xAngle = 0; xAngle < 360; xAngle += 30) { // Rotación alrededor del eje X
      push(); // Guarda el estado actual de transformaciones

      // Rota el cubo alrededor de los ejes Z y X
      rotateZ(zAngle);
      rotateX(xAngle);

      // Mueve los cubos lejos del centro (400 unidades en el eje Y)
      translate(0, 400, 0);

      // Dibuja un cubo
      box();

      pop(); // Restaura el estado de transformaciones anterior
    }
  }
}


1. **`setup()`**: Configura el lienzo en 3D, ajusta el color y grosor de las líneas, y describe el comportamiento del programa.
2. **`draw()`**: 
   - Establece el fondo rosa.
   - Permite mover la vista en 3D usando el ratón.
   - Crea una esfera de cubos que rotan alrededor de los ejes X y Z.
   
Cada cubo se dibuja en una posición específica en 3D, y los usuarios pueden verlos desde diferentes ángulos arrastrando el ratón.
```
#### Modificacion del codigo 
```
function setup() {
  createCanvas(710, 400, WEBGL); // Crea un lienzo en 3D de 710x400 píxeles
  angleMode(DEGREES); // Usa grados en lugar de radianes para los ángulos
  strokeWeight(2); // Grosor de las líneas (aunque se desactiva después)
  stroke(255, 200, 150); // Color de borde cálido (pero no se usa porque quitamos los bordes)
  
  // Descripción del código
  describe('Puedes hacer clic y arrastrar para ajustar la vista 3D. Hay una esfera formada por pequeñas esferas sobre un fondo degradado azul.');
}

function draw() {
  // Crea un fondo degradado de azul oscuro a azul claro
  for (let i = 0; i < height; i++) {
    let inter = map(i, 0, height, 0, 1); // Interpolación entre 0 y 1
    let c = lerpColor(color(0, 50, 150), color(135, 206, 250), inter); // Genera el degradado
    stroke(c); // Define el color de la línea
    line(-width / 2, i - height / 2, width / 2, i - height / 2); // Dibuja una línea horizontal
  }

  orbitControl(); // Permite mover la vista con el mouse o la pantalla táctil

  noStroke(); // Quita los bordes de las figuras
  fill(255, 150, 50); // Color de las esferas (naranja cálido)

  // Bucle para crear la esfera formada por pequeñas esferas
  for (let zAngle = 0; zAngle < 180; zAngle += 30) { // Rotación en el eje Z
    for (let xAngle = 0; xAngle < 360; xAngle += 30) { // Rotación en el eje X
      push(); // Guarda el estado de las transformaciones

      rotateZ(zAngle); // Rota la figura en el eje Z
      rotateX(xAngle); // Rota la figura en el eje X
      translate(0, 300, 0); // Posiciona las formas lejos del centro

      sphere(20); // Se cambió box() por sphere(), ahora son esferas de radio 20

      pop(); // Restaura el estado original de las transformaciones
    }
  }
}
```
Aprendi lo siguiente:

- **`setup()`**: Crea el lienzo en 3D y configura el grosor y color de los bordes.
- **`draw()`**: Dibuja un fondo degradado usando `for`, `map()`, y `lerpColor()`.
- **`orbitControl()`**: Permite mover la cámara con el ratón. Usamos `noStroke()` para eliminar bordes y `fill()` para darle color a las esferas.
- **`rotateX()` y `rotateZ()`**: Rota las esferas en los ejes X y Z. `translate()` mueve las esferas en el espacio.
- **`push()` y `pop()`**: Guardan y restauran las transformaciones para que no afecten a otras figuras.


