# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 01

#### ¿Qué es un sistema físico interactivo?

Es un sistema que implementa complementos fisicos y digitales para hacer experiencias de manera mas dinamicas.

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

En el mundo de las experiencias se puede usar de muchas maneras, ya sea para conciertos, alguna escena de una pelicula o un videojuego,
o alguna experiencia que requiera el uso del cuerpo y la tecnología.

### Actividad 02

#### ¿Qué es el diseño/arte generativo?

Es un tipo de arte que usa sistemas autonomos para generar obras basadas en alguna cosa, como un video para una cancion, quizas tambien
se pueda incluir ampliar una obra artistica como un cuadro, o incluso generar una obra de arte mediante un prompt y algunas lineas de codigo
donde se pueden configurar algunas caracteristicas de la obra. Estas mismas usan un conjunto de reglas en un software, una maquina o cualquier
procedimiento experimental. Este arte se caracteriza por estar hecho por una maquina con instrucciones humanas, la maquina dibuja y pinta, el 
humano programa que se se va a dibujar y de que colores se va a pintar.

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

la verdad es que esto se puede usar en cualquier cosa, ya sea en experiencias para mejorar visualmente un evento y la interaccion con este,
en los videojuegos se podria usar para casi todo, de igual manera con la animacion. Aparte, con estas herramientas podemos hacer nuestro trabajo
mucho mas facil.

### Actividad 03

Para hacer esta actividad, hicimos uso de un microbit y de unas aplicaciones llamadas microbit editor y p5.js. El input, proceso y el output de este
ejercicio no son tan dificiles de identificar en mi caso, el microbit es el input, el dispositivo que conectamos para poder realizar la actividad y que
carga su información al computador. El proceso se hizo en p5,js y microbit editor, con estas aplicaciones le dimos instrucciones a lo que el microbit debe
realizar, el corazon y la carita feliz que se vio en las luces, todo eso fue procesado en el computador con esas dos aplicaciones. Para finalizar, el output
seria la información del proceso cargada en el microbit, es decir, las luces led, ya que estas muestran el resultado de lo que hicimos en el proceso, el corazón
y la carita feliz.

### Actividad 04
[LINK P5JS](https://editor.p5js.org/Tomygga/sketches/7hMKzJwGH)

CODIGO
```
function setup() {
  createCanvas(600, 600);
}

function draw() {
  background(15);
  drawOjo();
  drawCuerpoDentroOjo();
}

function drawOjo()
{
  push();
  translate(width / 2, height / 2);
  noFill();
  stroke(1450);
  strokeWeight(10);
  ellipse(0, 0, 400, 400);
}

function drawCuerpoDentroOjo(){
  fill(255);
  ellipse(0, -50, 60, 60);
  rectMode(CENTER);
  rect(0, 40, 50, 100, 20);
  
  ellipse(-20, 90, 25, 100);     
  ellipse(20, 90, 25, 100);   
   ellipse(-35, 30, 20, 60);
  ellipse(35, 40, 20, 60);
  pop();

}
````
