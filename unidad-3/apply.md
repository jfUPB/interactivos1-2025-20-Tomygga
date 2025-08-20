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
