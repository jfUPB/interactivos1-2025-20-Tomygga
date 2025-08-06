# Unidad 2

## 🔎 Fase: Set + Seek

### ACTIVIDAD 1

````.py
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()
````
#### Describe detalladamente cómo funciona este ejemplo.
Este programa enciende y apaga dos luces leds del microbit, y basicamente funciona de la siguiente manera:

##### 1 CLASE PIXEL
Esta clase define el comportamiento de un pixel, ya sea sus coordenadas o si la luz led esta apagada o encendida. Tambien podria decirse que modela el pixel con un brillo entre 0 y 9.

##### 2 ATRIBUTOS Y METODO UPDATE
Los atributos de este codigo son basicamente las funciones que manejan el pixel, ya sean atributos como el pixelX y el pixelY que son para las coordenadas, interval que maneja el tiempo
que debe pasar para alternar el pixel de estado o tambien atributos como el startTime que es el momento donde se inician los conteos para los cambios de las luces.

En el caso del metodo update, este se usa para llamar al bucle principal para actualizar el estado del pixel, este mismo cuenta con dos estados (Init) y (WaitTimeout), donde el primer
estado se usa mas para guardar el tiempo actual, dibujar el pixel con un valor entre (0,9) y cambiar al siguiente estado, que funciona mas como para verificar si lo anterior es correcto
y mostrar el resultado en pantalla

##### 3 OBJETOS CREADOS
pixel1 y pixel2 son las 2 luces que el microbit enciende, donde el pixel 1 parpadea cada 1000 ms (1 s) y esta ubicado en (0,0), mientras que el pixel2 parpadea cada 500 ms (0.5 s) y 
este mismo esta ubicado en la posicion (4,4), estos mismos conforman el bucle principal del programa.

#### ¿Cuáles son los estados en el programa?
init y WaitTimeout, el primero como mencione anteriormente es el estado inicial del programa, que se encarga de guardar el tiempo y dibujar el pixel en su estado inicial, mientras que
el segundo espera a que pase ese tiempo anterior mencionado para alternar los estados de los pixeles y mostrarlos en pantalla.

#### ¿Cuáles son los eventos/inputs en el programa?
Este programa tiene un evento de tiempo de forma interna, que es cuando startTime sobrepasa a Interval, de resto, el programa no tiene algun input de forma externa.

#### ¿Cuáles son las acciones en el programa?
- Mostrar el estado inicial del pprograma (init)
- Esperar un tiempo determinado (WaitTimeout)
- alternar el estado de los pixeles (Encendido, apagado)(0,9)
- actualizar el led (display_set_pixel)

### ACTIVIDAD 2
````.py
from microbit import *
import utime

RED = "Red"
GREEN = "Green"
YELLOW = "Yellow"

estado = RED

def mostrar_estado(estado):
    display.clear()
    if estado == RED:
        display.set_pixel(2, 0, 9)  
    elif estado == YELLOW:
        display.set_pixel(2, 2, 9)  
    elif estado == GREEN:
        display.set_pixel(2, 4, 9)  


while True:
    mostrar_estado(estado)

    if estado == RED:
        utime.sleep(3)
        estado = GREEN
    elif estado == GREEN:
        utime.sleep(3)
        estado = YELLOW
    elif estado == YELLOW:
        utime.sleep(1)
        estado = RED
````
##### Estados
Serian Red, Yellow y Green, ya que estos representan los estados que tiene un semaforo pero un microbit, donde el estado inicial es Red.

##### Eventos
En este caso, los eventos vienen del paso del tiempo, es decir son implicitos:
- Después de 3 segundos en RED, ocurre el evento (Cambia a Green)
- Después de 3 segundos en GREEN, ocurre el evento (Cambia a Yellow)
- Después de 1 segundo en YELLOW, ocurre el evento (Cambia a Red)

Tambien esta el utime.sleep que con estos cambios de estado representan los eventos.

##### ACCIONES
````py
def mostrar_estado(estado):
    display.clear()
    if estado == RED:
        display.set_pixel(2, 0, 9)
    elif estado == YELLOW:
        display.set_pixel(2, 2, 9)
    elif estado == GREEN:
        display.set_pixel(2, 4, 9)
````
Son estos, se encargan de darle la posicion al led y mostrarlo en la pantalla.

### ACTIVIDAD 3
<img width="685" height="810" alt="image" src="https://github.com/user-attachments/assets/40da4ade-e540-479e-a11f-a03021c9f1f1" />

````.py
from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3

HAPPY_INTERVAL = 1500
SMILE_INTERVAL = 1000
SAD_INTERVAL = 2000

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    # pseudoestado STATE_INIT
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY
    elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            # Acciones para el evento
            display.show(Image.SAD)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            # Acciones para el evento
            display.show(Image.SMILE)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
    elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
           current_state = STATE_SAD
    elif current_state == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
````
#### Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.
Este programa simula las tareas de una manera concurrente al manejar los eventos y el tiempo de ambos a la vez sin detenerse, lo que permite que el 
programa de respuestas simultaneas.

#### Identifica los estados, eventos y acciones en el programa
ACCIONES:
- MOSTRAR IMAGEN
- CAMBIAR ESTADO
  
ESTADOS: 
- INIT
- HAPPY
- SMILE
- SAD

EVENTOS:
- PASO DEL TIEMPO
- BOTÓN A


#### Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario el sistema puede tener un error.

- Vector 1: INIT muestra happy y despues pasa a happy, pasa la prueba y es funcional.
- Vector 2: en smile cuando no se presionada nada se deja pasar el tiempo, despues muestra a sad y cambia a sad, pasa la prueba.
- Vector 3: En happy cuando se presiona muestra a sad y pasa a sad, prueba exitosa.











