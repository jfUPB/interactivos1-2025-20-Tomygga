# Unidad 2


## 🛠 Fase: Apply

### ACTIVIDAD 04
Diagrama del ejercicio:
<img width="1840" height="1480" alt="Diagrama en blanco" src="https://github.com/user-attachments/assets/0a51a857-14f9-4d5f-a288-69578a99d3f9" />

### ACTIVIDAD 05
#### CODIGO DEL EJERCICIO
````.py
from microbit import *
import utime

STATE_CONF = 0
STATE_ARMED = 1
STATE_BOOM = 2

current_state = STATE_CONF
start_time = 0
time_left = 20  

TIME_MIN = 10
TIME_MAX = 60

while True:
    
    if current_state == STATE_CONF:
        display.show(str(time_left))

        if button_a.was_pressed():
            if time_left < TIME_MAX:
                time_left += 1
            display.show(str(time_left))

        if button_b.was_pressed():
            if time_left > TIME_MIN:
                time_left -= 1
            display.show(str(time_left))

        if pin_logo.is_touched():
            time_left = 20
            display.show(str(time_left))

        if accelerometer.was_gesture("shake"):
            start_time = utime.ticks_ms()
            display.show(str(time_left))
            current_state = STATE_ARMED

    elif current_state == STATE_ARMED:
        if utime.ticks_diff(utime.ticks_ms(), start_time) >= 1000:
            start_time = utime.ticks_ms()
            time_left -= 1
            display.show(str(time_left))

        if time_left <= 0:
            current_state = STATE_BOOM
            display.show(Image.SKULL)

    elif current_state == STATE_BOOM:
        display.show(Image.SKULL)
        if pin_logo.is_touched():
            time_left = 20
            current_state = STATE_CONF
            display.show(str(time_left))
````

#### VECTORES DE PRUEBA

- Cuando se inicia deben salir los numeros de tiempo (20)
- Cuando se presione el boton shake tiene que empezar la cuenta regresiva
- Explosion cuando el tiempo llegue a 0
- Cuando llegue a 0 debe salir la imagen de skull


