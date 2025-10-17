
# Evidencias de la unidad 7

## ACTIVIDAD 1

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?
Este fue el link:

https://51c0043k-3000.use2.devtunnels.ms/

Lo que pasa es que el localhost es cuando abrimos el server en nuestro computador y la pagina solo se puede abrir desde este. Ya que como tal es un link local al que solo se puede acceder desde donde se abrio el server. En cambio con este "DevTunnels", ponemos a correr por asi decirlo un server que genera este link de donde se puede acceder de cualquier lado para probar la aplicación, eso si, si es desde el computador se agrega un /Desktop/ al link o si es del celular se añade un /mobile/

### Describe brevemente qué hace npm install y npm start.

npm install lo que hace es que busca y descarga las dependencias que el codigo necesita, en cambio npm start requiere que estas dependencias ya esten instaladas para que se pueda iniciar el servidor con "server.js". En resumen, npm start inicia el servidor con las dependencias que se instalan con npm install.

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

<img width="376" height="198" alt="image" src="https://github.com/user-attachments/assets/5abf3124-7bf9-4936-90d9-f7e015db6b1d" />

Es como un mensaje para los dos, ya que conecta el cliente del celular y el del computador, pero la consola solo reporta cuando uso el touch desde el celular para mover el circulo en la pantalla del computador.

### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?

https://github.com/user-attachments/assets/bdc6adc0-9d2a-431f-9625-7ddb82734830

Si funciono, desde el celular se hacen los movimientos y desde la pantalla del computador se mueve el circulo, pero si se nota que hay un poco de retraso entre la interacción del celular y el computador.

## ACTIVIDAD 2

### Explica con tus propias palabras: ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?
Porque Dev Tunnels lo que hace es que es un intermediario seguro que nos permite ingresar mediante una url publica al servidor que estamos corriendo desde el computador, cosa que con el localHost no sirve porque este solo corre un servidor en el dispositivo que se creo, por lo que en este caso, Dev Tunnels permite ingresar a un server de otro dispositivo de manera segura para interactuar.

### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
La función de touchMoved() lo que hace es que llama continuamentre mientras el usuario mantiene el dedo presionado y lo mueve en el recuadro del celular, donde mouseX y mouseY contienen las coordenadas actuales de donde se dirija el circulo con el toque.

El threshold es mas como para optimizar el codigo, ya que con esto el codigo no envia un mensaje por cada pequeño movimiento, sino que comprueba con lastTouchX y lastTouchY supera un limite, lo que evita que inunde la red de mensajes para que no reporte cosas que no son necesarias.
### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
Usar la IP local permite acceder a tu aplicación dentro de la misma red (LAN) sin depender de servicios externos. Es rápido, simple y ofrece el mejor rendimiento posible porque la conexión es directa entre dispositivos. Sin embargo, su alcance está limitado: solo funciona mientras todos los equipos estén en la misma red y el firewall lo permita. Además, normalmente no cuenta con HTTPS, lo que puede causar problemas al probar integraciones que requieren conexiones seguras.

Por otro lado, Dev Tunnels permite exponer tu servidor local a Internet mediante una URL pública y segura (HTTPS), sin necesidad de configurar puertos o redes. Es ideal para compartir tu app con otras personas o probar servicios que necesitan un callback remoto, como webhooks o autenticación OAuth. A cambio, introduce algo de latencia, depende de la estabilidad del servicio del túnel y la conexión puede expirar o requerir reactivación. En resumen, es más flexible y práctico, pero menos directo y estable que usar la IP local.

### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).

https://github.com/user-attachments/assets/f70da731-0a7e-4b04-99f4-1964c7efccd3

## ACTIVIDAD 3

### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?

La función princial de express.static(‘public’) es permitir que el servidor envie automaticamente los archivos estaticos ubicados en la carpeta public como los HTML o los javascript, sin necesidad de definir rutas manuales. A diferencia del otro que usamos (app.get) que requiere especificar la respuesta para cada solicitud de manera programada. Por eso, express.static sirve directamente para facilitar y reducir el codigo necesario en el servidor.

### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?

El flujo de un mensaje táctil inicia cuando el móvil detecta un evento de toque (por ejemplo, touchmove o touchstart) y lo envía al servidor mediante socket.emit('message', datos). El servidor recibe ese evento dentro del manejador socket.on, registra el mensaje con console.log y lo retransmite a los demás clientes conectados usando socket.broadcast.emit. Los demás dispositivos (por ejemplo, escritorios) reciben este mensaje mediante su propio socket.on, lo que les permite reaccionar en tiempo real a la interacción del móvil. Se utiliza socket.broadcast.emit porque envía el mensaje a todos los clientes excepto al emisor, evitando que el móvil reciba su propio mensaje duplicado.

### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?

Si conectas dos computadores de escritorio y un celular al servidor, cuando el celular emita un mensaje táctil, este será recibido únicamente por los dos escritorios. Esto ocurre porque el servidor usa socket.broadcast.emit, que retransmite el mensaje a todos los demás clientes conectados excepto al que lo envió. En consecuencia, el celular no verá su propio mensaje reflejado, mientras que los demás dispositivos sí lo recibirán y podrán procesarlo.

### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?

Los mensajes console.log en el servidor proporcionan información útil para monitorear el comportamiento de la aplicación en tiempo real. Permiten saber cuándo un cliente se conecta o se desconecta, cuándo se recibe un mensaje y cuál es su contenido. Esto facilita la depuración, el seguimiento del flujo de datos y la verificación de que los eventos entre los distintos clientes y el servidor se están produciendo correctamente.

## ACTIVIDAD 4
### DIAGRAMA 

<img width="2091" height="951" alt="image" src="https://github.com/user-attachments/assets/d20e49ef-4feb-4431-9930-c6738ac79a00" />

## APPLY
### IDEA
Voy a hacer un viaje espacial, la canción que elegi para esta ocasión fue astrothunder de travis scott.

[ASTROTHUNDER](https://www.youtube.com/watch?v=Pa67b28h0vY&list=RDPa67b28h0vY&start_radio=1)

Como tal va a ver una nave espacial que se puede controlar con el touch del movil solo las posiciones verticales, que va a ir viajando por un fondo del espacio con estrellas, nebulosas, planetas y meteoritos, que van a ir golpeando a la nave espacial hasta quitarle la vida, donde si la nave por asi decirlo muere, la canción se para y deja la nave flotando a la deriva. Lo que va a reaccionar a la canción principalmente van a ser las nebulosas que van a ir aumentando su tamaño o bajando dependiendo de los sintetizadores de la canción, como tal quiero que el usuario mientras ve la interacción con la canción, vaya esquivando los meteoritos para poder terminar la canción. Aparte, la velocidad de la nave depende de la canción.

<img width="1166" height="729" alt="image" src="https://github.com/user-attachments/assets/c4a8aa03-19bb-4429-aed2-8b981fb9873b" />

Esto es una inspiración, no va a disparar ni nada porque la canción es como muy relajada como tal.

### PROBLEMAS

El codigo me fue bien y todo, el unico problema es que por alguna razon la canción inicia solo con el click y no con el touch, a pesar de que con el touch si inicie el viaje.

### DESKTOP.js/html

```js
let fft, song;
let audioStarted = false;

let socket;
let lastTouchTime = 0;
let targetY = null; 

let stars = [];
let nebulas = [];
let planets = [];


let ship;

let yellowShiftActive = false;
let yellowShiftStart = 0;
let yellowShiftDuration = 2000;

let colorShiftActive = false;
let colorShiftStart = 0;
let colorShiftDuration = 2000;
let hueOffset = 0;

let nextAutoShift = 0;
let autoShiftInterval = 25000;

let meteorites = [];
let lightningBolts = []; 
let health = 100;
let gameOver = false;


function preload() {
  soundFormats('mp3', 'ogg');
  song = loadSound('../astrothunder.mp3');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  angleMode(DEGREES);
  colorMode(RGB);


  for (let i = 0; i < 300; i++) {
    stars.push(new Star());
  }


  for (let i = 0; i < 6; i++) nebulas.push(new Nebula());


  for (let i = 0; i < 5; i++) {
    planets.push(new Planet(random(width * 0.2, width * 1.5), random(height), random(40, 160)));
  }

  ship = new Ship(width * 0.2, height / 2);

  fft = new p5.FFT(0.8, 256);
  nextAutoShift = millis() + autoShiftInterval;

  socket = io();
  socket.on('connect', () => console.log('Connected to server'));

  socket.on('message', (data) => {
    if (data.type === 'touch') {
      lastTouchTime = millis();
      targetY = data.y;
    } else if (data.type === 'yellowShift') {
      yellowShiftActive = true;
      yellowShiftStart = millis();
    } else if (data.type === 'touchEnd') {
      targetY = null;
    } else if (data.type === 'start') {
      if (!audioStarted && !gameOver) {
        try {
          userStartAudio();
          song.loop();
          audioStarted = true;
          console.log('Audio started from mobile START');
        } catch (e) {
          console.warn('userStartAudio failed', e);
        }
      }
    }
  });

  socket.on('disconnect', () => console.log('Disconnected'));

  for (let i = 0; i < 8; i++) meteorites.push(new Meteorite());
}

function draw() {
  let spectrum = [];
  if (audioStarted) spectrum = fft.analyze();
  let bass = audioStarted ? fft.getEnergy('bass') : 0;
  let mid = audioStarted ? fft.getEnergy('mid') : 0;
  let treble = audioStarted ? fft.getEnergy('treble') : 0;

  drawSpaceBackground(bass);


  if (millis() > nextAutoShift) {
    colorShiftActive = true;
    colorShiftStart = millis();
    nextAutoShift = millis() + autoShiftInterval;
  }

  if (colorShiftActive) {
    let elapsed = millis() - colorShiftStart;
    let progress = constrain(elapsed / colorShiftDuration, 0, 1);
    hueOffset = lerp(0, 160, progress);
    if (progress >= 1) colorShiftActive = false;
  } else hueOffset = 0;

  if (bass > 220 && !colorShiftActive) {
    colorShiftActive = true;
    colorShiftStart = millis();
  }


  for (let n of nebulas) {
    n.reactToMid(mid);
    n.update();
    n.display();
  }

  for (let p of planets) {
    p.reactToEnergy(mid, treble);
    p.update(bass);
    p.display();
  }

if (audioStarted) {
  
  let energyMix = (treble * 0.6 + mid * 0.3 + bass * 0.1);

  let prob = map(energyMix, 0, 255, 0, 0.8);
  if (random() < prob * 0.15) {
    let count = floor(map(energyMix, 100, 255, 1, 4, true));
    for (let i = 0; i < count; i++) {
      lightningBolts.push(new Lightning(bass, treble));
    }
  }
}

for (let i = lightningBolts.length - 1; i >= 0; i--) {
  lightningBolts[i].update();
  lightningBolts[i].display();
  if (lightningBolts[i].done) lightningBolts.splice(i, 1);
}

  if (!gameOver) {
    for (let m of meteorites) {
      m.update(bass);
      m.display();
      if (m.hits(ship)) {
        health -= map(bass, 0, 255, 1.2, 3.2);
        m.reset();
      }
    }
  }

  ship.reactToMusic(bass, treble);
  if (targetY && millis() - lastTouchTime < 500) {
    ship.moveToY(lerp(ship.pos.y, targetY, 0.18));
  } else ship.updateInertia();
  ship.display();

  for (let s of stars) {
    s.reactToTreble(treble);
    s.update(bass);
    s.display();
  }

  if (yellowShiftActive) {
    let elapsed = millis() - yellowShiftStart;
    let progress = constrain(elapsed / yellowShiftDuration, 0, 1);
    push();
    blendMode(ADD);
    noStroke();
    fill(255, 230, 120, map(1 - abs(progress - 0.5) * 2, 0, 1, 0, 120));
    rect(0, 0, width, height);
    pop();
    if (elapsed > yellowShiftDuration * 2) yellowShiftActive = false;
  }

  if (!audioStarted) drawStartScreen();

  drawHealthBar();
  if (health <= 0 && !gameOver) {
    gameOver = true;
    if (song && song.isPlaying()) song.pause();
    console.log('GAME OVER - song paused');
  }
}

function drawStartScreen() {
  push();
  fill(255);
  textAlign(CENTER, CENTER);
  textSize(32);
  text('PRESIONA PARA EMPEZAR', width / 2, height / 2);
  pop();
}

function mousePressed() {
  if (!audioStarted && !gameOver) {
    userStartAudio();
    song.loop();
    audioStarted = true;
  }
}

function touchStarted() {
  lastTouchTime = millis();

  if (!audioStarted && !gameOver) {
    try {
      userStartAudio();
      song.loop();
      audioStarted = true;
      console.log('Audio started from mobile touch');
    } catch (e) {
      console.warn('userStartAudio failed', e);
    }
  }

  if (touches.length > 0) targetY = touches[0].y;

  return false; 
}

function touchMoved() {
  lastTouchTime = millis();
  if (touches.length > 0) targetY = touches[0].y;
  return false;
}
function touchEnded() {
  targetY = null;
  return false;
}


class Star {
  constructor() { this.reset(true); }
  reset(initial = false) {
    this.x = random(-width * 0.2, width * 1.2);
    this.y = random(-height * 0.2, height * 1.2);
    this.baseSize = random(0.6, 2.6);
    this.size = this.baseSize;
    this.twinkle = random(TWO_PI);
    this.speedFactor = random(0.05, 0.6);
    if (!initial) {
      if (random() < 0.5) this.x = width + random(50, 400);
      else this.x = -random(50, 400);
      this.y = random(height);
    }
  }
  reactToTreble(t) {
    this.size = this.baseSize + map(t, 0, 255, 0, 2) * (0.5 + sin(frameCount * 0.08 + this.twinkle) * 0.5);
  }
  update(b) {
    let speed = map(b, 0, 255, 0.2, 6) * this.speedFactor;
    this.x -= speed;
    if (this.x < -100) this.reset();
  }
  display() {
    push();
    noStroke();
    fill(255, 255, 255, map(this.size, 0.5, 4, 80, 255));
    ellipse(this.x, this.y, this.size);
    pop();
  }
}

class Nebula {
  constructor() { this.reset(); }
  reset() {
    this.x = random(width * 0.3, width * 1.2);
    this.y = random(height * 0.1, height * 0.9);
    this.baseRadius = random(120, 420);
    this.radius = this.baseRadius * 0.2;
    this.h = random(180, 300);
    this.s = random(60, 100);
    this.b = random(30, 90);
    this.alpha = 0;
  }
  reactToMid(m) {
    let targetAlpha = map(m, 0, 255, 0, 120);
    this.alpha = lerp(this.alpha, targetAlpha, 0.08);
    this.radius = lerp(this.radius, this.baseRadius * (1 + map(m, 0, 255, 0, 0.9)), 0.06);
  }
  update() {
    this.x -= 0.15 + sin(frameCount * 0.003 + this.y) * 0.05;
    this.y += sin(frameCount * 0.002 + this.x) * 0.1;
    if (this.x < -this.radius) this.reset();
  }
  display() {
    push();
    translate(this.x, this.y);
    blendMode(ADD);
    noStroke();
    for (let r = this.radius; r > 0; r -= this.radius / 6) {
      let a = map(r, 0, this.radius, 0, this.alpha) * 0.9;
      fill(this.h + hueOffset * 0.2, this.s, this.b, a);
      ellipse(0, 0, r, r * 0.6);
    }
    blendMode(BLEND);
    pop();
  }
}

class Planet {
  constructor(x, y, r) {
    this.pos = createVector(x, y);
    this.r = r;
    this.baseR = r;
    this.color = { h: random(10, 360), s: random(40, 90), b: random(40, 95) };
    this.visibleAlpha = 0;
    this.speed = random(0.02, 0.6);
  }
  reactToEnergy(mid, treble) {
    let energy = max(mid, treble);
    let target = map(energy, 0, 255, 0, 200);
    this.visibleAlpha = lerp(this.visibleAlpha, target, 0.08);
  }
  update(bass) {
    this.pos.x -= map(bass, 0, 255, 0.2, 6) * this.speed;
    if (this.pos.x < -this.baseR * 2) {
      this.pos.x = random(width + 100, width * 1.6);
      this.pos.y = random(height * 0.1, height * 0.9);
    }
  }
  display() {
    push();
    translate(this.pos.x, this.pos.y);
    noStroke();
    blendMode(ADD);
    for (let i = 5; i > 0; i--) {
      let rr = this.r * (i / 5);
      let a = map(i, 0, 5, 0, this.visibleAlpha) * 0.12;
      fill(this.color.h + hueOffset * 0.1, this.color.s, this.color.b, a);
      ellipse(0, 0, rr * 2, rr * 1.6);
    }
    blendMode(BLEND);
    fill(this.color.h + hueOffset * 0.1, this.color.s, this.color.b, 200);
    ellipse(0, 0, this.r * 2, this.r * 1.6);
    noFill();
    stroke(255, map(this.visibleAlpha, 0, 255, 0, 150));
    strokeWeight(1.2);
    ellipse(0, 0, this.r * 2.6, this.r * 1.95);
    pop();
  }
}

class Ship {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.velY = 0;
    this.w = 100;
    this.h = 40;
    this.baseSpeed = 0.8;
    this.bassBoost = 0;
    this.glow = 0;
  }
  reactToMusic(b, t) {
    this.bassBoost = map(b, 0, 255, 0, 7);
    this.glow = map(b, 0, 255, 0, 160);
    this.vib = sin(frameCount * 0.6) * map(t, 0, 255, 0, 3);
  }
  moveToY(y) {
    let target = constrain(y, this.h, height - this.h);
    this.pos.y = target;
    this.velY = 0;
  }
  updateInertia() {
    this.velY *= 0.93;
    this.pos.y += this.velY;
    this.pos.y = constrain(this.pos.y, this.h, height - this.h);
  }
  display() {
    push();
    translate(this.pos.x, this.pos.y + (this.vib || 0));
    push();
    blendMode(ADD);
    noStroke();
    fill(80, 160, 255, this.glow);
    ellipse(-this.w * 0.35, 0, this.w * 0.8, this.h * 0.9);
    pop();
    noStroke();
    fill(20, 30, 60);
    rectMode(CENTER);
    rect(0, 0, this.w, this.h, 18);
    fill(40, 120, 200);
    beginShape();
    vertex(this.w * 0.3, -this.h * 0.25);
    vertex(this.w * 0.55, 0);
    vertex(this.w * 0.3, this.h * 0.25);
    endShape(CLOSE);
    fill(150, 220, 255, 200);
    ellipse(this.w * 0.03, 0, this.w * 0.45, this.h * 0.6);
    fill(30, 60, 90);
    triangle(-this.w * 0.15, -this.h * 0.55, this.w * 0.2, 0, -this.w * 0.15, this.h * 0.55);
    push();
    translate(-this.w * 0.6, 0);
    fill(255, 120, 60, map(this.glow, 0, 180, 30, 220));
    beginShape();
    vertex(-10, -6);
    vertex(-40 - this.bassBoost * 2, 0);
    vertex(-10, 6);
    endShape(CLOSE);
    pop();
    pop();
  }
}

function drawSpaceBackground(b) {
  for (let y = 0; y <= height; y += 6) {
    let inter = map(y, 0, height, 0, 1);
    let c1 = color(10, 12, 30);
    let c2 = color(0, 0, 10);
    let c = lerpColor(c1, c2, inter);
    noStroke();
    fill(c);
    rect(0, y, width, 6);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

class Meteorite {
  constructor() { this.reset(); }
  reset() {
    this.x = random(width, width * 1.5);
    this.y = random(0, height);
    this.size = random(28, 80);
    this.speed = random(2, 5);
  }
  update(b) {
    this.x -= this.speed + map(b, 0, 255, 0, 3);
    this.y += sin(frameCount * 0.02 + this.x * 0.01) * 0.4;
    if (this.x < -this.size) this.reset();
  }
  display() {
    push();
    translate(this.x, this.y);
    noStroke();
    fill(120, 100, 80);
    ellipse(0, 0, this.size);
    fill(255, 100);
    ellipse(0, 0, this.size * 0.45);
    pop();
  }
  hits(ship) {
    let d = dist(this.x, this.y, ship.pos.x, ship.pos.y);
    return d < (this.size / 2 + max(ship.w, ship.h) * 0.5);
  }
}

function drawHealthBar() {
  push();
  noStroke();
  fill(40, 40, 40, 160);
  rect(width * 0.05, height * 0.06, width * 0.4, 18, 6);
  fill(255, 90, 90);
  let w = map(constrain(health, 0, 100), 0, 100, 0, width * 0.4);
  rect(width * 0.05, height * 0.06, w, 18, 6);
  fill(255);
  textSize(12);
  textAlign(LEFT, CENTER);
  text('VIDA', width * 0.05, height * 0.06 - 10);
  pop();
}

class Lightning {
  constructor(bass = 0, treble = 0) {
    this.x1 = random(width * 0.3, width * 0.9);
    this.y1 = random(height * 0.1, height * 0.9);
    this.x2 = this.x1 + random(-80, 80);
    this.y2 = this.y1 + random(100, 250);
    this.alpha = 255;
    this.life = 0;
    this.done = false;

    this.intensity = map(treble, 0, 255, 0.3, 1);
    this.colorShift = map(bass, 0, 255, 0, 100);
  }
  update() {
    this.life++;
    this.alpha -= 20;
    if (this.alpha <= 0) this.done = true;
  }
  display() {
    push();
    stroke(150 + this.colorShift, 200, 255, this.alpha);
    strokeWeight(random(2, 4) * this.intensity);
    noFill();

    beginShape();
    let steps = int(random(4, 7));
    let xStep = (this.x2 - this.x1) / steps;
    let yStep = (this.y2 - this.y1) / steps;
    let x = this.x1, y = this.y1;
    vertex(x, y);
    for (let i = 0; i < steps; i++) {
      x += xStep + random(-8, 8);
      y += yStep + random(-10, 10);
      vertex(x, y);
    }
    endShape();
    pop();
  }
}
```
```.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Desktop p5.js Application</title>

  <!-- Librerías principales -->
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>

  <!-- Socket.IO -->
  <script src="/socket.io/socket.io.js"></script>

  <!-- Tu sketch -->
  <script src="sketch.js"></script>
</head>
<body></body>
</html>
```

### MOBILE.JS/HTML
```js
let socket;
let lastTouchX = null;
let lastTouchY = null;
let started = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);
  socket = io();

  socket.on('connect', () => console.log('Connected to server'));
}

function draw() {
  background(10, 12, 30); 
  fill(200);
  textAlign(CENTER, CENTER);
  textSize(18);

  if (!started) {
    text('TOCA PARA INICIAR EL VIAJE 🚀', width / 2, height / 2);
  } else {
    text(
      'MANTÉN PRESIONADO PARA MOVER LA NAVE (VERTICAL)\nPULSA PARA DESTELLO AMARILLO',
      width / 2,
      height / 2
    );
  }
}

function touchStarted() {
  if (socket && socket.connected && touches.length > 0) {
    let t = touches[0];
    lastTouchX = t.x;
    lastTouchY = t.y;

    if (!started) {
      socket.emit('message', { type: 'start' });
      started = true;
      if (window.navigator.vibrate) window.navigator.vibrate(50);
    }

    socket.emit('message', { type: 'touch', x: t.x, y: t.y });
    socket.emit('message', { type: 'yellowShift' });
  }
  return false;
}

function touchMoved() {
  if (socket && socket.connected && touches.length > 0) {
    let t = touches[0];
    lastTouchX = t.x;
    lastTouchY = t.y;

    socket.emit('message', { type: 'touch', x: t.x, y: t.y });
  }
  return false;
}

function touchEnded() {
  if (socket && socket.connected) {
    socket.emit('message', { type: 'touchEnd' });
  }
  return false;
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
```.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <script src="sketch.js"></script>
    <title>Mobile p5.js Application</title>
</head>
<body></body>
</html>

```




















