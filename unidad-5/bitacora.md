
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

### Captura el resultado del experimento anterior. Lo que ves ¿Cómo está relacionado con esta línea de código?
```cpp
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
```
Al seleccionar todo en Hex, se ven nuemeros hecadecimales como (FF 85 01 C8 00 01), esto esta relacionado al codigo por el struct.pack, que convierte los valores en binario y la aplicacion SerialTerminal muestra esos bytes en Hexadecimal. 

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


















