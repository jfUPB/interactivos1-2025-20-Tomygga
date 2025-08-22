# Unidad 3


## 🛠 Fase: Apply

## ACTIVIDAD 6
CODIGO DE LA BOMBA 2.0 EN P5.JS
```.js
let PASSWORD = ['A', 'B', 'A'];
let key = [];
let keyIndex = 0;
let count = 20;
let startTime;
let state = "CONFIGURACION"; 

let btnA, btnB, btnShake, btnReset;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);
  startTime = millis();

  btnA = createButton('A');
  btnA.position(50, height + 20);
  btnA.mousePressed(() => handleButton('A'));

  btnB = createButton('B');
  btnB.position(100, height + 20);
  btnB.mousePressed(() => handleButton('B'));

  btnShake = createButton('Shake');
  btnShake.position(150, height + 20);
  btnShake.mousePressed(() => handleShake());

  btnReset = createButton('Reset');
  btnReset.position(220, height + 20);
  btnReset.mousePressed(() => handleReset());
}

function draw() {
  background(30);
  fill(255);

  if (state === "CONFIGURACION") {
    text("CONFIGURACION", width / 2, 50);
    text(count, width / 2, height / 2);

  } else if (state === "ARMADO") {
    text("ARMADO", width / 2, 50);
    text(count, width / 2, height / 2);

    if (millis() - startTime > 1000) {
      startTime = millis();
      count--;
      if (count <= 0) {
        state = "EXPLOSION";
      }
    }

  } else if (state === "EXPLOSION") {
    text("💀💀💥💥💥💥💀💀", width / 2, height / 2);
  }
}

function handleButton(btn) {
  if (state === "CONFIGURACION") {
    if (btn === 'A') {
      count = min(count + 1, 60);
    } else if (btn === 'B') {
      count = max(10, count - 1);
    }
  } else if (state === "ARMADO") {
    key[keyIndex] = btn;
    keyIndex++;

    if (keyIndex === PASSWORD.length) {
      let passIsOK = true;
      for (let i = 0; i < PASSWORD.length; i++) {
        if (key[i] !== PASSWORD[i]) 
        {
          passIsOK = false;
          break;
        }
      }

      if (passIsOK) 
      {
        count = 20;
        state = "CONFIGURACION";
      }
      keyIndex = 0;
      key = [];
    }
  }
}

function handleShake() {
  if (state === "CONFIGURACION") {
    startTime = millis();
    state = "ARMADO";
  }
}

function handleReset() {
  if (state === "EXPLOSION") {
    count = 20;
    startTime = millis();
    state = "CONFIGURACION";
  }
}
```
## ACTIVIDAD 7

### CODIGO P5.JS

```.js
let bombTask;
let serialTask;
let event;
let port;
let connectBtn;

function setup(){
  createCanvas(400,400);
  textAlign(CENTER,CENTER);
  textSize(32);

  port = createSerial();
  connectBtn = createButton('Connect To Microbit');
  connectBtn.position(130,300);
  connectBtn.mousePressed(connectBtnClick);

  event = new paraBailarEstoEsUnaBombaEvent();
  bombaTask = new BombaTask();
  serialTask = new SerialTask();
}

function draw(){
  background(0);

  serialTask.update();
  bombaTask.update();

  bombaTask.display();
}

class paraBailarEstoEsUnaBombaEvent {
  constructor(){
    this.value = null;
  }
  set(val){ this.value = val; }
  clear(){ this.value = null; }
  read(){ return this.value; }
}

class SerialTask {
  update(){
    if(port.availableBytes() > 0){
      let dataRx = port.read(1);
      if(dataRx === 'A') event.set('A');
      else if(dataRx === 'B') event.set('B');
      else if(dataRx === 'S') event.set('S');
      else if(dataRx === 'T') event.set('T');
    }

    if (!port.opened()) connectBtn.html('Connect to micro:bit');
    else connectBtn.html('Disconnect');
  }
}

class BombaTask {
  constructor(){
    this.PASSWORD = ['A','B','A'];
    this.key = [];
    this.count = 20;
    this.startTime = millis();
    this.state = 'CONFIGURACION';
  }

  update(){
    if(this.state === 'CONFIGURACION'){
      if(event.read() === 'A'){
        event.clear();
        this.count = min(this.count + 1, 60);
      }
      else if(event.read() === 'B'){
        event.clear();
        this.count = max(this.count - 1, 10);
      }
      else if(event.read() === 'S'){
        event.clear();
        this.startTime = millis();
        this.state = 'ARMADO';
      }
    }

    else if(this.state === 'ARMADO'){
      if(millis() - this.startTime > 1000){
        this.count--;
        this.startTime = millis();
        if(this.count <= 0){
          this.state = 'EXPLOSION';
        }
      }

      if(event.read() === 'A' || event.read() === 'B'){
        this.key.push(event.read());
        event.clear();
        if(this.key.length === this.PASSWORD.length){
          if(this.key.join('') === this.PASSWORD.join('')){
            this.state = 'CONFIGURACION';
            this.count = 20;
          }
          this.key = [];
        }
      }
    }

    else if(this.state === 'EXPLOSION'){
      if(event.read() === 'T'){
        event.clear();
        this.state = 'CONFIGURACION';
        this.count = 20;
        this.startTime = millis();
      }
    }
  }

  display(){
    fill(255);
    if(this.state === 'CONFIGURACION'){
      text(`CONFIGURACION\n${this.count}`, width/2, height/2);
    }
    else if(this.state === 'ARMADO'){
      text(`ARMADO\n${this.count}`, width/2, height/2);
    }
    else if(this.state === 'EXPLOSION'){
      fill(255,0,0);
      text("EXPLOSION", width/2, height/2);
    }
  }
}

function connectBtnClick(){
  if(!port.opened()){
    port.open('MicroPython',115200);
  } else {
    port.close();
  }
}

function keyPressed() {
  if (key === 'A') event.set('A');
  else if (key === 'B') event.set('B');
  else if (key === 'S') event.set('S');
  else if (key === 'T') event.set('T');
}
```
### LINK A LA WEB
[LINK P5.JS](https://editor.p5js.org/Tomygga/sketches/fizBbhkgS)

### CODIGO DEL MICROBIT

```python
from microbit import *

uart.init(baudrate=115200)
display.show(Image.HAPPY)

while True:
    display.show(Image.HAPPY)
    if button_a.was_pressed():
        uart.write('A')
        display.show(Image.ARROW_N)
        sleep(200)
    if button_b.was_pressed():
        uart.write('B')
        display.show(Image.ARROW_S)
        sleep(200)
    if accelerometer.was_gesture('shake'):
        uart.write('S')
        display.show(Image.SAD)
        sleep(200)
    if pin_logo.is_touched():
        uart.write('T')
        display.show(Image.HAPPY)
        sleep(200)
```




