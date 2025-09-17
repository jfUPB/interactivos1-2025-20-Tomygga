
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

### 

## Actividad 02










