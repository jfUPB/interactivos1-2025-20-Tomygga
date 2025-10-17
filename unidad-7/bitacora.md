
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


















