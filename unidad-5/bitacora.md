
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




