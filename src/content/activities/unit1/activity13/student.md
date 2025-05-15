##### 
# Sonido generativo básico

### Codigo 
```
let osc;
let waveType = 'sine'; // Tipo de onda inicial
let freq = 440; // Frecuencia inicial en Hz

function setup() {
  createCanvas(400, 400);
  
  // Crear un oscilador
  osc = new p5.Oscillator();
  osc.setType(waveType);
  osc.freq(freq);
  osc.amp(0.5); // Volumen
  osc.start();
}

function draw() {
  background(220);
  textSize(16);
  text('Presiona 1: Seno, 2: Triangular, 3: Cuadrado', 10, 20);
  text('Presiona A: Subir frecuencia, B: Bajar frecuencia', 10, 40);
  text('Frecuencia actual: ' + freq + ' Hz', 10, 60);
  text('Tipo de onda actual: ' + waveType, 10, 80);
}

function keyPressed() {
  if (key === '1') {
    waveType = 'sine';
    osc.setType(waveType);
  } else if (key === '2') {
    waveType = 'triangle';
    osc.setType(waveType);
  } else if (key === '3') {
    waveType = 'square';
    osc.setType(waveType);
  } else if (key === 'a' || key === 'A') {
    freq += 10; // Aumentar frecuencia en 10 Hz
    osc.freq(freq);
  } else if (key === 'b' || key === 'B') {
    freq -= 10; // Disminuir frecuencia en 10 Hz
    osc.freq(freq);
  }
}

```

![image](https://github.com/user-attachments/assets/fda7ed88-366d-4939-8783-3f6aa4e44f87)
