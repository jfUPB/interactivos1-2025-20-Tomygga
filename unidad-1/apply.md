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
#### Explicación código

El Sistema fisico interactivo de esta actividad lo que hace es usar los botones del microbit para hacer un cambio de color en un cuadrado que aparecera en la pantalla,
y que cuando suelten el boton, este vuelva a su color original. Para ello voy a hacer una explicacion de los codigos que nos dieron y asi explicar como funciona el sistema
fisico interactivo. (Me imagino que es esto)

##### PARTE 1: MICROBIT 
Para poder hacer uso del microbit, lo que necesitamos hacer es primero programarlo y subir la información al microbit, para que esta misma pueda ser
usada mas adelante para lo que vamos a hacer.
````
  from microbit import *

from microbit import *

uart.init(baudrate=115200)

while True:

    if button_a.is_pressed():
        uart.write('A')
    else:
        uart.write('N')

    sleep(100)
````
Este primer codigo lo que hace es configurar el boton del microbit, en las primeras dos instrucciones del codigo, estas envian información al microbit para
poder programar lo demas, la arte del while true, es un bucle en el cual busca que cuando presionemos el boton A, verifique si desde la ultima comprobación 
este mismo fue presionado antes, si usaramos el was y no el is, este mismo buscaría si el boton fue presionado en la ultima comprobacion, en vez de preguntarse
si esta siendo presionado en ese mismo momento. La parte donde aparece la N es para que cuando se suelte el boton del microbit, este mismo vuelva al color original
del cuadrado, es decir, es como si hicieramos un interruptor de apagar y prender una luz, pero si soltamos el boton la luz se apaga.

En resumen, este codigo nos sirve para que el microbit y la computadora sepan que presionamos el boton A y asi poder usarlo para lo que vamos a hacer a futuro. Aparte
de que tambien esta lo de que cuando soltemos el boton, el cuadrado vuelva al color original.

##### PARTE 2: CÓDIGO EN P5JS
````
  let port;
  let connectBtn;
  let connectionInitialized = false;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        fill("red");
      } else if (dataRx == "N") {
        fill("green");
      }
    }

    rectMode(CENTER);
    rect(width / 2, height / 2, 50, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
````
Esto vendria siendo el codigo completo para lo que queremos hacer, pero ¿Como funciona?

Antes de responder esto, cabe recalcar que para hacer este codigo es necesario implementar la siguiente libreria para que funcione:
````
<script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
````
Ahora si. En este codigo lo que se busca es dibujar un canvas de 400x400, y que cuando presionemos el boton A del microbit, este cambie de color y al soltarlo
vuelva a su color original.

Para poder explicar como funciona el código, lo voy a hacer función por función, como en el código. Empezando con la función Setup() esta lo que hace es que crea
el canvas donde se va a dibujar, crea el fondo de un color gris claro. Tambien se encarga de crear la comunicacion con el microbit, con lo del boton connecto to 
microbit, su ubicación en el canvas y que se pueda hacer click en este boton

En la función Draw() se dibuja el cuadrado, se revisa el puerto y este mismo busca actuar con los datos recibidos (BOTON A O SI NO ESTA PRESIONADO N), Basicamente la funcion
Setup() es como un molde, mientras que la función Draw() es con la que el proyecto que estamos haciendo pueda funcionar, ya que este mismo dibuja, revisa y actua en base a 
los datos que le llegan.

Para finalizar con la funcion connectBtnClick(), esta lo que hace es ejecutarse cuando el usuario hace  clic en el boton, si el puerto no esta abierto, este lo abre y lo marca
para que pueda inicializarse en la funcion Draw(), y si el puerto esta abierto este lo cierra.
