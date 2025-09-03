# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](https://editor.p5js.org/generative-design/sketches/H1oflc9q6kV)

Código a modificar:

``` js
// P_2_3_7_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * Simple drawing tool where mouse input gets mirrored over multiple axes
 *
 * MOUSE
 * left click          : draw line
 *
 * KEYS
 * 1                   : toggle vertical mirror
 * 2                   : toggle horizontal mirror
 * 3                   : toggle diagonal mirror 1
 * 4                   : toggle diagonal mirror 2
 * 5-9                 : change color
 * 0                   : color white (eraser)
 * arrow up            : increase line weight
 * arrow down          : decrease line weight
 * arrow right         : increase number of tiles
 * arrow left          : decrease number of tiles
 * d                   : show/hide mirror axes
 * del, backspace      : clear screen
 * g                   : start/stop gif recording
 * s                   : save png
 *
 * CONTRIBUTED BY
 * [Niels Poldervaart](http://NielsPoldervaart.nl)
*/
'use strict';

var gif;
var canvasElement;
var recording = false;

var lineWidth = 3;
var lineColor;

var mv = true;
var mh = true;
var md1 = true;
var md2 = true;
var penCount = 1;

var showAxes = true;

var img;

function setup() {
  // Please work with a square canvas
  canvasElement = createCanvas(800, 800);
  noCursor();
  noFill();
  lineColor = color(0);

  // Create an offscreen graphics object to draw into
  img = createGraphics(width, height);
  img.pixelDensity(1);

  setupGIF();
}

function draw() {
  background(255);
  image(img, 0, 0);

  img.strokeWeight(lineWidth);
  img.stroke(lineColor);

  if (mouseIsPressed && mouseButton == LEFT) {
    var w = width / penCount;
    var h = height / penCount;
    var x = mouseX % w;
    var y = mouseY % h;
    var px = x - (mouseX - pmouseX);
    var py = y - (mouseY - pmouseY);

    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var ox = i * w;
        var oy = j * h;

        // Normal position
        img.line(x + ox, y + oy, px + ox, py + oy);
        // Horizontal mirror or all three other mirrors
        if (mh || md2 && md1 && mv) img.line(w - x + ox, y + oy, w - px + ox, py + oy);
        // Vertical mirror
        if (mv || md2 && md1 && mh) img.line(x + ox, h - y + oy, px + ox, h - py + oy);
        // Horizontal and vertical mirror
        if (mv && mh || md2 && md1) img.line(w - x + ox, h - y + oy, w - px + ox, h - py + oy);

        // When mirroring diagonally, flip X and Y inputs.
        if (md1 || md2 && mv && mh) img.line(y + ox, x + oy, py + ox, px + oy);
        if (md1 && mh || md2 && mv) img.line(y + ox, w - x + oy, py + ox, w - px + oy);
        if (md1 && mv || md2 && mh) img.line(h - y + ox, x + oy, h - py + ox, px + oy);
        if (md1 && mv && mh || md2) img.line(h - y + ox, w - x + oy, h - py + ox, w - px + oy);
      }
    }

    if (recording) {
      gif.addFrame(canvasElement.canvas, {delay: 1, copy: true});
    }
  }

  if (showAxes) {
    var w = width / penCount;
    var h = height / penCount;

    // draw mirror axes and tiles
    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var x = i * w;
        var y = j * h;

        stroke(0, 50);
        strokeWeight(1);
        if (mh) line(x + w / 2, y, x + w / 2, y + h);
        if (mv) line(x, y + h / 2, x + w, y + h / 2);
        if (md1) line(x, y, x + w, y + h);
        if (md2) line(x + w, y, x, y + h);

        stroke(15, 233, 118, 50);
        strokeWeight(1);
        rect(i * w, j * h, w - 1, h - 1);
      }
    }

    // draw pen
    fill(lineColor);
    noStroke();
    ellipse(mouseX, mouseY, lineWidth + 2, lineWidth + 2);
    stroke(0, 50);
    noFill();
    ellipse(mouseX, mouseY, lineWidth + 1, lineWidth + 1);
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) img.clear();

  if (keyCode == RIGHT_ARROW) penCount++;
  if (keyCode == LEFT_ARROW) penCount = max(1, penCount - 1);

  if (keyCode == UP_ARROW) lineWidth++;
  if (keyCode == DOWN_ARROW) lineWidth = max(1, lineWidth - 1);

  if (key == '1') mv = !mv;
  if (key == '2') mh = !mh;
  if (key == '3') md1 = !md1;
  if (key == '4') md2 = !md2;

  if (key == '5') lineColor = color(0);
  if (key == '6') lineColor = color(15, 233, 118);
  if (key == '7') lineColor = color(245, 95, 80);
  if (key == '8') lineColor = color(65, 105, 185);
  if (key == '9') lineColor = color(255, 231, 108);
  if (key == '0') lineColor = color(255);

  if (key == 'd' || key == 'D') showAxes = !showAxes;
  if (key == 'g' || key == 'G') {
    recording = !recording;
    if (!recording) {
      gif.render();
    }
  }
}

function setupGIF() {
  background(255);
  gif = new GIF({
    workers: 16,
    quality: 10000,
    debug: true,
    workerScript: '../../libraries/gif.js/gif.worker.js'
  });
  gif.on('finished', function(blob) {
    saveAs(blob, gd.timestamp() + '.gif');
    setupGIF();
  });
}

```

[Enlace a la aplicación modificada](https://editor.p5js.org/generative-design/sketches/P_2_3_7_01)

Código modificado:

``` js
// P_2_3_7_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * Simple drawing tool where mouse input gets mirrored over multiple axes
 *
 * MOUSE
 * left click          : draw line
 *
 * KEYS
 * 1                   : toggle vertical mirror
 * 2                   : toggle horizontal mirror
 * 3                   : toggle diagonal mirror 1
 * 4                   : toggle diagonal mirror 2
 * 5-9                 : change color
 * 0                   : color white (eraser)
 * arrow up            : increase line weight
 * arrow down          : decrease line weight
 * arrow right         : increase number of tiles
 * arrow left          : decrease number of tiles
 * d                   : show/hide mirror axes
 * del, backspace      : clear screen
 * g                   : start/stop gif recording
 * s                   : save png
 *
 * CONTRIBUTED BY
 * [Niels Poldervaart](http://NielsPoldervaart.nl)
*/
'use strict';

var gif;
var canvasElement;
var recording = false;

var lineWidth = 3;
var lineColor;

var overrideSMouseY = 0
var mv = true;
var mh = true;
var md1 = true;
var md2 = true;
var penCount = 1;

var showAxes = true;

var img;

function setup() {
  // Please work with a square canvas
  canvasElement = createCanvas(800, 800);
  noCursor();
  noFill();
  lineColor = color(0);

  // Create an offscreen graphics object to draw into
  img = createGraphics(width, height);
  img.pixelDensity(1);

  setupGIF();
}

function draw() {
  background(255);
  image(img, 0, 0);

  img.strokeWeight(lineWidth);
  img.stroke(lineColor);

  if (mouseIsPressed && mouseButton == LEFT) {
    var w = width / penCount;
    var h = height / penCount;
    var x = mouseX % w;
    var y = mouseY % h;
    var px = x - (mouseX - pmouseX);
    var py = y - (mouseY - pmouseY);

    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var ox = i * w;
        var oy = j * h;

        // Normal position
        img.line(x + ox, y + oy, px + ox, py + oy);
        // Horizontal mirror or all three other mirrors
        if (mh || md2 && md1 && mv) img.line(w - x + ox, y + oy, w - px + ox, py + oy);
        // Vertical mirror
        if (mv || md2 && md1 && mh) img.line(x + ox, h - y + oy, px + ox, h - py + oy);
        // Horizontal and vertical mirror
        if (mv && mh || md2 && md1) img.line(w - x + ox, h - y + oy, w - px + ox, h - py + oy);

        // When mirroring diagonally, flip X and Y inputs.
        if (md1 || md2 && mv && mh) img.line(y + ox, x + oy, py + ox, px + oy);
        if (md1 && mh || md2 && mv) img.line(y + ox, w - x + oy, py + ox, w - px + oy);
        if (md1 && mv || md2 && mh) img.line(h - y + ox, x + oy, h - py + ox, px + oy);
        if (md1 && mv && mh || md2) img.line(h - y + ox, w - x + oy, h - py + ox, w - px + oy);
      }
    }

    if (recording) {
      gif.addFrame(canvasElement.canvas, {delay: 1, copy: true});
    }
  }

  if (showAxes) {
    var w = width / penCount;
    var h = height / penCount;

    // draw mirror axes and tiles
    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var x = i * w;
        var y = j * h;

        stroke(0, 50);
        strokeWeight(1);
        if (mh) line(x + w / 2, y, x + w / 2, y + h);
        if (mv) line(x, y + h / 2, x + w, y + h / 2);
        if (md1) line(x, y, x + w, y + h);
        if (md2) line(x + w, y, x, y + h);

        stroke(15, 233, 118, 50);
        strokeWeight(1);
        rect(i * w, j * h, w - 1, h - 1);
      }
    }

    // draw pen
    fill(lineColor);
    noStroke();
    ellipse(mouseX, mouseY, lineWidth + 2, lineWidth + 2);
    stroke(0, 50);
    noFill();
    ellipse(mouseX, mouseY, lineWidth + 1, lineWidth + 1);
  }
}

function keyPressed() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) img.clear();

  if (keyCode == RIGHT_ARROW) penCount++;
  if (keyCode == LEFT_ARROW) penCount = max(1, penCount - 1);

  if (keyCode == UP_ARROW) lineWidth++;
  if (keyCode == DOWN_ARROW) lineWidth = max(1, lineWidth - 1);

  if (key == '1') mv = !mv;
  if (key == '2') mh = !mh;
  if (key == '3') md1 = !md1;
  if (key == '4') md2 = !md2;

  if (key == '5') lineColor = color(0);
  if (key == '6') lineColor = color(15, 233, 118);
  if (key == '7') lineColor = color(245, 95, 80);
  if (key == '8') lineColor = color(65, 105, 185);
  if (key == '9') lineColor = color(255, 231, 108);
  if (key == '0') lineColor = color(255);

  if (key == 'd' || key == 'D') showAxes = !showAxes;
  if (key == 'g' || key == 'G') {
    recording = !recording;
    if (!recording) {
      gif.render();
    }
  }
}

function setupGIF() {
  background(255);
  gif = new GIF({
    workers: 16,
    quality: 10000,
    debug: true,
    workerScript: '../../libraries/gif.js/gif.worker.js'
  });
  gif.on('finished', function(blob) {
    saveAs(blob, gd.timestamp() + '.gif');
    setupGIF();
  });
}

// ----------- MICROBIT SERIAL INTEGRATION -----------
let port;
let reader;
let microbitX = 0;
let microbitY = 0;
let buttonA = 0;
let buttonB = 0;

let lastButtonBTime = 0;
let colorIndex = 0;
let colors = []; // Inicializo vacío para definir en setup

// Override mouse variables
let overrideMouseX = 0;
let overrideMouseY = 0;
let isDrawing = false;

let connectButton;

function setup() {
  createCanvas(800, 800);
  noCursor();
  noFill();

  // Defino colores aquí que p5 ya está listo
  colors = [
    color(0),           // Negro
    color(255, 0, 0),   // Rojo
    color(0, 255, 0),   // Verde
    color(0, 0, 255),   // Azul
    color(255, 255, 0), // Amarillo
    color(255, 0, 255), // Magenta
    color(0, 255, 255), // Cian
    color(0)            // Negro otra vez
  ];
  
  lineColor = colors[0];

  img = createGraphics(width, height);
  img.pixelDensity(1);

  setupGIF();

  // Crear botón para conectar
  connectButton = createButton('Conectar al micro:bit');
  connectButton.position(10, 10);
  connectButton.mousePressed(connectToMicrobit);
}

function connectToMicrobit() {
  navigator.serial.requestPort().then(selectedPort => {
    port = selectedPort;
    return port.open({ baudRate: 115200 });
  }).then(() => {
    reader = port.readable.getReader();
    readSerial();
    connectButton.html("Conectado");
    connectButton.attribute("disabled", "");
  }).catch(err => {
    console.error('Error al conectar al micro:bit:', err);
    alert("No se pudo conectar al micro:bit.");
  });
}

function readSerial() {
  reader.read().then(({ value, done }) => {
    if (done) {
      reader.releaseLock();
      return;
    }

    let data = new TextDecoder().decode(value);
    processSerial(data);
    readSerial(); // Loop
  });
}

let serialBuffer = "";

function processSerial(data) {
  serialBuffer += data;

  let lines = serialBuffer.split("\n");
  while (lines.length > 1) {
    const line = lines.shift().trim();
    const parts = line.split(",");
    if (parts.length === 4) {
      microbitX = parseInt(parts[0]);
      microbitY = parseInt(parts[1]);
      buttonA = parseInt(parts[2]);
      let newButtonB = parseInt(parts[3]);

      // Detectar doble clic en botón B
      if (newButtonB === 1 && buttonB === 0) {
        let now = millis();
        if (now - lastButtonBTime < 400) {
          img.clear(); // Doble clic -> borrar
        } else {
          // Cambio de color
          colorIndex = (colorIndex + 1) % colors.length;
          lineColor = colors[colorIndex];
        }
        lastButtonBTime = now;
      }
      buttonB = newButtonB;
    }
  }
  serialBuffer = lines.join("\n");
}

// Variables auxiliares para dibujo (debes definirlas si no las tienes)

let pmouseX = 0;
let pmouseY = 0;

function draw() {
  background(255);
  image(img, 0, 0);

  // Mapear acelerómetro a posición del canvas
  overrideMouseX = map(microbitX, -1024, 1024, 0, width);
  overrideMouseY = map(microbitY, -1024, 1024, 0, height);

  img.strokeWeight(lineWidth);
  img.stroke(lineColor);

  if (buttonA === 1) {
    var w = width / penCount;
    var h = height / penCount;
    var x = overrideMouseX % w;
    var y = overrideMouseY % h;
    var px = x - (overrideMouseX - pmouseX);
    var py = y - (overrideMouseY - pmouseY);

    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var ox = i * w;
        var oy = j * h;

        img.line(x + ox, y + oy, px + ox, py + oy);
        if (mh || (md2 && md1 && mv)) img.line(w - x + ox, y + oy, w - px + ox, py + oy);
        if (mv || (md2 && md1 && mh)) img.line(x + ox, h - y + oy, px + ox, h - py + oy);
        if ((mv && mh) || (md2 && md1)) img.line(w - x + ox, h - y + oy, w - px + ox, h - py + oy);

        if (md1 || (md2 && mv && mh)) img.line(y + ox, x + oy, py + ox, px + oy);
        if ((md1 && mh) || (md2 && mv)) img.line(y + ox, w - x + oy, py + ox, w - px + oy);
        if ((md1 && mv) || (md2 && mh)) img.line(h - y + ox, x + oy, h - py + ox, px + oy);
        if ((md1 && mv && mh) || md2) img.line(h - y + ox, w - x + oy, h - py + ox, w - px + oy);
      }
    }
  }

  if (showAxes) {
    var w = width / penCount;
    var h = height / penCount;

    for (var i = 0; i < penCount; i++) {
      for (var j = 0; j < penCount; j++) {
        var x = i * w;
        var y = j * h;

        stroke(0, 50);
        strokeWeight(1);
        if (mh) line(x + w / 2, y, x + w / 2, y + h);
        if (mv) line(x, y + h / 2, x + w, y + h / 2);
        if (md1) line(x, y, x + w, y + h);
        if (md2) line(x + w, y, x, y + h);

        stroke(15, 233, 118, 50);
        strokeWeight(1);
        rect(i * w, j * h, w - 1, h - 1);
      }
    }

    fill(lineColor);
    noStroke();
    ellipse(overrideMouseX, overrideMouseY, lineWidth + 2, lineWidth + 2);
    stroke(0, 50);
    noFill();
    ellipse(overrideMouseX, overrideSMouseY, lineWidth + 1, lineWidth + 1);
  }

  pmouseX = overrideMouseX;
  pmouseY = overrideMouseY;
}
```

## Video

[Video demostratativo](URL)



