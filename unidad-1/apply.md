# Unidad 1

## 🛠 Fase: Apply
### Actividad 06
[link P5JS](https://editor.p5js.org/Tomygga/sketches/PhUJj3nog)

#### Codigo Microbit editor
```
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write('A')  
    elif button_b.is_pressed():
        uart.write('B')
    else:
        uart.write('N')  
    sleep(100)
```
#### Codigo P5JS
```
let port;
let connectBtn;
let connectionInitialized = false;
let x;

function setup() 
{
  createCanvas(400, 400);
  background(220);
  x = width / 2;

  port = createSerial();
  connectBtn = createButton("Conectar micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() 
{
  background(220);
  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }

  if (port.availableBytes() > 0) 
  {
    let char = port.read(1);
    if (char === "A") {
      x -= 20;
    } else if (char === "B") {
      x += 20;
    }
    x = constrain(x, 0, width);
  }

  ellipse(x, height / 2, 100,100);

  if (!port.opened()) 
  {
    connectBtn.html("Conectar micro:bit");
  } 
  else 
  {
    connectBtn.html("Desconectar");
  }
}

function connectBtnClick() 
{
  if (!port.opened()) 
  {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } 
  else 
  {
    port.close();
  }
}
```
### Actividad 05




