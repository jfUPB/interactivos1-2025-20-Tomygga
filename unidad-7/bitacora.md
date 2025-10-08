
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

### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).











