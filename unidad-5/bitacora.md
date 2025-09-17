
# Evidencias de la unidad 5

## ACTIVIDAD 1

### Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?
El micro:bit y el sketch se comunican a traves del puerto serial UART,  en el editor de python se usa el UART para enviar datos a 115200 baudios donde y en el sketch toca agregar la biblioteca de p5webserial para que funcione; y no solo eso, para que pueda recibir los datos del micro:bit tiene que usarse port.readUntil ("\n")-

Los datos que envia el micro:bit al sketch son:
- El estado del boton A
- El estado del boton B
- Las coordenadas del acelereomtro de (x,y) para que funcione como una especie de cursor.

### ¿Cómo es la estructura del protocolo ASCII usado?
La estructura del protocolo ASCII en este codigo se ve asi:
```cpp
xValue, yValue, aState, bState\n
```
Donde:
- xValue es el numero entero que representa la posición horizontal del micro:bit
- yValue representa la posición vertical
- aState que indica si el boton A esta presionado o no
- bState es lo mismo que el a solo que con el boton B :D

### Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.
```cpp
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    }
  }
}

```
El codigo lee los datos enviados por el microbit a traves del puerto serial usando el port.readUntil, lo que devuelve una linea completa como "23, -15, true, false", despues de esto se limpia con trim y se separa en un arreglo con split, obteniendo de este cuatro valores X, Y y los estados del boton A y B. Los dos primeros se convierten en enteros y se les suma el windowWidth y el windowHeight para que el punto inicial o central del microbit (0,0) quede en el centro del lienzo del p5, logrando que los movimientos que se hagan se traduzcan a coordenadas en pantalla. Los valores del boton A y B son booleanos y se pasan a la funcion updatebuttonstates, que se encarga de generar las acciones correspondientes al detectar una pulsacion(true) o liberacion(false).

### ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?

Los estados del boton A y B se generan en p5 comparando el estado actual de los botones con su estado anterior. Donde el microbit manda en serie los valores de los botones A y B (true o false) y p5 guarda esos valores e microBitAState y microBitBstate para compararlos en updateButtonStates donde A pressed ocurre cuando antes estaban false y ahora llega a true, y el B released ocurre cuand antes estaba en true y ahora llega a false. Una vez detectada la transicion, se ejecuta el bloque correspondiente y se muestra un mensaje en consola donde indica si los botones estan presionados o liberados. Es decir, los eventos se generan por transicion de estado, no es suficiente con que el microbit diga que A esta en true, sino que el p5 detecte el cambio de la fase.

### Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

<img width="876" height="808" alt="20250917_141813" src="https://github.com/user-attachments/assets/bc91797e-26c3-4342-a123-557c510ce642" />
<img width="876" height="808" alt="20250917_141927" src="https://github.com/user-attachments/assets/6c31dfee-01cd-4a78-b80b-9447e89b8a6e" />
<img width="876" height="808" alt="20250917_142026" src="https://github.com/user-attachments/assets/89ff21a2-3fcb-433f-8af3-fdee235f7e7b" />

## Actividad 02

### Captura el resultado del experimento anterior. ¿Por qué se ve este resultado?

Porque cuando seleccionamos texto en la aplicacion SerialTerminal, los datos se ven como números separados por comas y esto se ve asi porque el microbit esta enviando los datos como ASCII (Texto plano), donde cada numero y coma se codifican en caracteres que se pueden leer facil como si fuera un mensaje de texto.

<img width="990" height="252" alt="image" src="https://github.com/user-attachments/assets/56201149-b32f-4008-bcd8-bc5f4823b493" />


### Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?
```cpp
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
```
Al seleccionar todo en Hex, se ven nuemeros hecadecimales como (FF 85 01 C8 00 01), esto esta relacionado al codigo por el struct.pack, que convierte los valores en binario y la aplicacion SerialTerminal muestra esos bytes en Hexadecimal. 

<img width="989" height="248" alt="image" src="https://github.com/user-attachments/assets/c2993663-80a3-4a93-852d-accb4161ec82" />

###  ¿Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?
#### Ventajas
- Ocupa menos espacio y se envian menos bytes
- Es mas rapido y eficiente para la comunicacion en el programa
- Es mas facil de procesar con programas como p5 porque no hay que convertir de texto a numero.

#### Desventajas

- Es mas dificil de leer por una persona normal
- Si se quiere revisar los datos a simple vista, no se entienden porque aparecen coo simbolos raros Hex

### Cuántos bytes se están enviando por mensaje? ¿Cómo se relaciona esto con el formato '>2h2B'? ¿Qué significa cada uno de los bytes?

El >2h2B es la parte del codigo que significa:

- 2h son dos enteros cortos, osea dos bytes cada uno
- 2B son dos enteros de un byte cada uno, osea son dos bytes en total y seis bytes por mensaje

Donde los bytes significa tienen diferente significado, donde se envian seis bytes por cada mensaje:

- dos bytes -> xValue
- dos bytes -> yValue
- un byte -> estado del boton A
- un byte -> estado del boton B

Estos bytes representan la informacion compactada. Cuando el numero es negativo, se usa complemento a dos, es decir se representan los numeros enteros negativos en binario.

### Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían los números negativos en el formato '>2h2B'?

Digamos que xValue es -123, en binario no se envia el signo como tal, sino que se representa con complemento a dos en dos bytes. Entonces en Hex se veria algo como FF 85. Esto significa que aunque en ASCII se veria como -123, en binario se ve un valor que esta modificado de otra manera, pero que al decodificarlo da el numero negativo correcto.

### ¿Qué diferencias ves entre los datos en ASCII y en binario? ¿Qué ventajas y desventajas ves en cada formato?

El ASCII se ve como un texto normal o claro (-123) mientras que en binario se ven como bytes en Hex (FF 85), aunque no tengan una diferencia mas que yo vea, estas serian las desventajas y ventajas:

#### Ventajas del binario

- Mas rapido de enviar
- Mas eficiente para el PC

#### Desventaja del binario
- Es muy complejo de leer.

#### Ventajas del ASCII
- Es mas facil de leer y entender
- Es mas util para hacer pruebas rapidas

#### Desventajas del ASCII

- Ocupa mas espacio
- Es mas lento porque envia mas caracteres

Por esto, el binario es mejor cuando se necesita eficiencia y rapidez, mientras que el ASCII es mejor cuando se quieren leer datos mas faciles para hacer pruebas.

### ACTIVIDAD 03

### ACTIVIDAD 04

### Construccion de la aplicacion
Este codigo es el de la aplicacion de la unidad pasada
```.js
'use strict';

let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAIT_MICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

let lastBPressTime = 0;
let bPressInterval = 400; 
let bPressCount = 0;

let canvasElement;
let img;
let lineWidth = 3;
let lineColor;
let mv = true, mh = true, md1 = true, md2 = true;
let penCount = 1;
let showAxes = true;

let smoothX = 0;
let smoothY = 0;
let pmouseX = 0;
let pmouseY = 0;
let smoothing = 0.2;

function setup() {
  canvasElement = createCanvas(800, 800);
  noCursor();
  noFill();
  lineColor = color(0);

  img = createGraphics(width, height);
  img.pixelDensity(1);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  if (newAState && !prevmicroBitAState) {
    print("A pressed → start drawing");
  }

  if (newBState && !prevmicroBitBState) {
    let currentTime = millis();
    if (currentTime - lastBPressTime < bPressInterval) {
      bPressCount++;
    } else {
      bPressCount = 1;
    }
    lastBPressTime = currentTime;

    if (bPressCount === 2) {
      img.clear();
      background(255);
      print("B double pressed → clear screen");
      bPressCount = 0;
    } else {
      let colors = [
        color(0),
        color(15, 233, 118),
        color(245, 95, 80),
        color(65, 105, 185),
        color(255, 231, 108),
        color(255),
      ];
      lineColor = colors[int(random(colors.length))];
      print("B pressed → change color");
    }
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + width / 2;
          microBitY = int(values[1]) + height / 2;
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
        }
      }
    }
  }

  smoothX = lerp(smoothX, microBitX, smoothing);
  smoothY = lerp(smoothY, microBitY, smoothing);

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      if (microBitConnected) {
        print("Microbit ready to draw");
        appState = STATES.RUNNING;
      }
      break;

    case STATES.RUNNING:
      if (!microBitConnected) {
        print("Waiting microbit connection");
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }

      background(255);
      image(img, 0, 0);

      img.strokeWeight(lineWidth);
      img.stroke(lineColor);

      if (microBitAState) {
        let w = width / penCount;
        let h = height / penCount;
        let x = smoothX % w;
        let y = smoothY % h;
        let px = x - (smoothX - pmouseX);
        let py = y - (smoothY - pmouseY);

        for (let i = 0; i < penCount; i++) {
          for (let j = 0; j < penCount; j++) {
            let ox = i * w;
            let oy = j * h;

            img.line(x + ox, y + oy, px + ox, py + oy);
            if (mh || (md2 && md1 && mv))
              img.line(w - x + ox, y + oy, w - px + ox, py + oy);
            if (mv || (md2 && md1 && mh))
              img.line(x + ox, h - y + oy, px + ox, h - py + oy);
            if ((mv && mh) || (md2 && md1))
              img.line(w - x + ox, h - y + oy, w - px + ox, h - py + oy);

            if (md1 || (md2 && mv && mh))
              img.line(y + ox, x + oy, py + ox, px + oy);
            if ((md1 && mh) || (md2 && mv))
              img.line(y + ox, w - x + oy, py + ox, w - px + oy);
            if ((md1 && mv) || (md2 && mh))
              img.line(h - y + ox, x + oy, h - py + ox, px + oy);
            if ((md1 && mv && mh) || md2)
              img.line(h - y + ox, w - x + oy, h - py + ox, w - px + oy);
          }
        }
      }

      if (showAxes) {
        let w = width / penCount;
        let h = height / penCount;

        for (let i = 0; i < penCount; i++) {
          for (let j = 0; j < penCount; j++) {
            let x = i * w;
            let y = j * h;

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
        ellipse(smoothX, smoothY, lineWidth + 2, lineWidth + 2);
        stroke(0, 50);
        noFill();
        ellipse(smoothX, smoothY, lineWidth + 1, lineWidth + 1);
      }

      pmouseX = smoothX;
      pmouseY = smoothY;
  }
}

function keyPressed() {
  if (keyCode == RIGHT_ARROW) penCount++;
  if (keyCode == LEFT_ARROW) penCount = max(1, penCount - 1);

  if (keyCode == UP_ARROW) lineWidth++;
  if (keyCode == DOWN_ARROW) lineWidth = max(1, lineWidth - 1);

  if (key == 'd' || key == 'D') showAxes = !showAxes;
}
```
Como tal, hay que modificar la aplicacion para que soporte el protocolo de datos binarios. El funcionamiento del programa tiene que ser el mismo, que dibuje como si tuviera 4 espejos, y como estamos en esta parte de datos, lo que tenemos que cambiar es esta parte:

```.js
let data = port.readUntil("\n");
if (data) {
  data = data.trim();
  let values = data.split(",");
  if (values.length == 4) {
    ...
  }
}
```
Esta es la que se encarga de los datos por asi decirlo, pero esta en texto ASCII, asi que tenemos que hacerle el cambio para que funcione con los datos binarios. Asi que, cogemos el codigo de microbit python que esta para hacer ese cambio en esta unidad y toca cambiar esta parte para que funcione por binarios, y tambien que se vea mas fluido que el programa anterior:

```.js
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0, 0, 9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    checksum = sum(data) % 256
    packet = b'\xAA' + data + bytes([checksum])
    uart.write(packet)
    sleep(100)
```

ACTUALIZACION: ya con el codigo final hecho, se modifico el draw para que quedara asi y funcione con binarios:

```.js
function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    while (port.availableBytes() >= 8) {   // esperar al menos 8 bytes
      let buffer = port.readBytes(8);

      if (buffer && buffer.length === 8) {
        if (buffer[0] === 0xAA) {
          let dataBytes = buffer.slice(1, 7);
          let checksum = buffer[7];

          let calcSum = dataBytes.reduce((a, b) => a + b, 0) % 256;
          if (calcSum === checksum) {
            let xRaw = (dataBytes[0] << 8) | (dataBytes[1] & 0xFF);
            if (xRaw & 0x8000) xRaw = xRaw - 0x10000; // signo

            let yRaw = (dataBytes[2] << 8) | (dataBytes[3] & 0xFF);
            if (yRaw & 0x8000) yRaw = yRaw - 0x10000; // signo

            let aState = dataBytes[4] !== 0;
            let bState = dataBytes[5] !== 0;

            microBitX = int(xRaw) + width / 2;
            microBitY = int(yRaw) + height / 2;
            microBitAState = aState;
            microBitBState = bState;

            updateButtonStates(microBitAState, microBitBState);
          }
        }
      }
    }
  }

  // resto del draw queda igual 
  smoothX = lerp(smoothX, microBitX, smoothing);
  smoothY = lerp(smoothY, microBitY, smoothing);
}
```
ya en parte de la construcción esto es todo.

### PRUEBAS INTERMEDIAS

La primera prueba es obviamente ver si el microbit y el codigo que se dio en el apply, funcionen, el cual fue efectivo jsdjsadja.

<img width="1114" height="946" alt="image" src="https://github.com/user-attachments/assets/4e3151af-88fb-4c96-aeb0-d3da57a5c63b" />

Si no lo hacia no era posible avanzar en el codigo. La siguiente prueba fue para ver que pasaba si ejecutaba el programa cuando quitaba la parte de la data que no nos sirve en este caso.

<img width="1919" height="945" alt="image" src="https://github.com/user-attachments/assets/68a3fb3a-611f-4890-bb4b-e68d2e15d87a" />

Al quitarla, el codigo seguia funcionando a casi toda su totalidad, permitia la conexion del microbit y el canvas con su espejo, la cosa es que al no estar enviando nada no puede dibujar, asi que hay que ponerse en la de empezar a codificar las cosas de los datos binarios.

<img width="1724" height="799" alt="image" src="https://github.com/user-attachments/assets/4bba8f2e-b0d1-4451-a1e2-3a735c649b7d" /> 
ahi puse la parte de la cabecera y su validacion, el codigo todavia no dibuja. Pero ya haciendo el checksum y haciendo el mapeo para que aparezca el cursor dibuje, acabe y de verdad dibuja con mas fluidez que el ejercicio de la unidad anterior

<img width="1793" height="762" alt="image" src="https://github.com/user-attachments/assets/d261f7c5-5299-47c1-8be0-dd9071945f16" />

Y ya ahi acabe el codigo de la unidad pasada con lo que vimos en esta unidad, de igual manera el microbit funciona como cursor y con A se dibujo, con B se cambia de color y si se presiona dos veces se borra, de resto, no hay ps nada mas que hacer no es tan largo.

### ERRORES
La verdad es que al ser un codigo tan corto no tuve casi errores, solo tuve uno y fue bastante sencillo de corregir, era este:

<img width="883" height="801" alt="image" src="https://github.com/user-attachments/assets/afb939bc-a84a-45c1-9031-50a138ccae81" />

Simplemente se corregia cambiando esta parte de 0x100 a 0x10000 en esta parte y ya, un fallo tonto mio.

De resto, el codigo al ser tan corto no me dio errores, de hecho lo hice bastante rapido y ya pues, asi quedo

### CODIGO FINAL
```.js
'use strict';

let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAIT_MICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

let lastBPressTime = 0;
let bPressInterval = 400;
let bPressCount = 0;

let canvasElement;
let img;
let lineWidth = 3;
let lineColor;
let mv = true, mh = true, md1 = true, md2 = true;
let penCount = 1;
let showAxes = true;

let smoothX = 0;
let smoothY = 0;
let pmouseX = 0;
let pmouseY = 0;
let smoothing = 0.2;

function setup() {
  canvasElement = createCanvas(800, 800);
  noCursor();
  noFill();
  lineColor = color(0);

  img = createGraphics(width, height);
  img.pixelDensity(1);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  if (newAState && !prevmicroBitAState) {
    print("A pressed → start drawing");
  }

  if (newBState && !prevmicroBitBState) {
    let currentTime = millis();
    if (currentTime - lastBPressTime < bPressInterval) {
      bPressCount++;
    } else {
      bPressCount = 1;
    }
    lastBPressTime = currentTime;

    if (bPressCount === 2) {
      img.clear();
      background(255);
      print("B double pressed → clear screen");
      bPressCount = 0;
    } else {
      let colors = [
        color(0),
        color(15, 233, 118),
        color(245, 95, 80),
        color(65, 105, 185),
        color(255, 231, 108),
        color(255),
      ];
      lineColor = colors[int(random(colors.length))];
      print("B pressed → change color");
    }
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    while (port.availableBytes() >= 8) {
      let buffer = port.readBytes(8);

      if (buffer && buffer.length === 8) {
        if (buffer[0] === 0xAA) {
          let dataBytes = buffer.slice(1, 7);
          let checksum = buffer[7];

          let calcSum = dataBytes.reduce((a, b) => a + b, 0) % 256;
          if (calcSum === checksum) {
            let xRaw = (dataBytes[0] << 8) | (dataBytes[1] & 0xFF);
            if (xRaw & 0x8000) xRaw = xRaw - 0x10000;

            let yRaw = (dataBytes[2] << 8) | (dataBytes[3] & 0xFF);
            if (yRaw & 0x8000) yRaw = yRaw - 0x10000;

            let aState = dataBytes[4] !== 0;
            let bState = dataBytes[5] !== 0;

            microBitX = int(xRaw) + width / 2;
            microBitY = int(yRaw) + height / 2;
            microBitAState = aState;
            microBitBState = bState;

            updateButtonStates(microBitAState, microBitBState);
          }
        }
      }
    }
  }

  smoothX = lerp(smoothX, microBitX, smoothing);
  smoothY = lerp(smoothY, microBitY, smoothing);

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      if (microBitConnected) {
        print("Microbit ready to draw");
        appState = STATES.RUNNING;
      }
      break;

    case STATES.RUNNING:
      if (!microBitConnected) {
        print("Waiting microbit connection");
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }

      background(255);
      image(img, 0, 0);

      img.strokeWeight(lineWidth);
      img.stroke(lineColor);

      if (microBitAState) {
        let w = width / penCount;
        let h = height / penCount;
        let x = smoothX % w;
        let y = smoothY % h;
        let px = x - (smoothX - pmouseX);
        let py = y - (smoothY - pmouseY);

        for (let i = 0; i < penCount; i++) {
          for (let j = 0; j < penCount; j++) {
            let ox = i * w;
            let oy = j * h;

            img.line(x + ox, y + oy, px + ox, py + oy);
            if (mh || (md2 && md1 && mv))
              img.line(w - x + ox, y + oy, w - px + ox, py + oy);
            if (mv || (md2 && md1 && mh))
              img.line(x + ox, h - y + oy, px + ox, h - py + oy);
            if ((mv && mh) || (md2 && md1))
              img.line(w - x + ox, h - y + oy, w - px + ox, h - py + oy);

            if (md1 || (md2 && mv && mh))
              img.line(y + ox, x + oy, py + ox, px + oy);
            if ((md1 && mh) || (md2 && mv))
              img.line(y + ox, w - x + oy, py + ox, w - px + oy);
            if ((md1 && mv) || (md2 && mh))
              img.line(h - y + ox, x + oy, h - py + ox, px + oy);
            if ((md1 && mv && mh) || md2)
              img.line(h - y + ox, w - x + oy, h - py + ox, w - px + oy);
          }
        }
      }

      if (showAxes) {
        let w = width / penCount;
        let h = height / penCount;

        for (let i = 0; i < penCount; i++) {
          for (let j = 0; j < penCount; j++) {
            let x = i * w;
            let y = j * h;

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
        ellipse(smoothX, smoothY, lineWidth + 2, lineWidth + 2);
        stroke(0, 50);
        noFill();
        ellipse(smoothX, smoothY, lineWidth + 1, lineWidth + 1);
      }

      pmouseX = smoothX;
      pmouseY = smoothY;
  }
}

function keyPressed() {
  if (keyCode == RIGHT_ARROW) penCount++;
  if (keyCode == LEFT_ARROW) penCount = max(1, penCount - 1);

  if (keyCode == UP_ARROW) lineWidth++;
  if (keyCode == DOWN_ARROW) lineWidth = max(1, lineWidth - 1);

  if (key == 'd' || key == 'D') showAxes = !showAxes;
}
```






















