
# Evidencias de la unidad 6

## ACTIVIDAD 01

### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?

<img width="856" height="182" alt="image" src="https://github.com/user-attachments/assets/0d0047d1-e3a0-4b62-a549-0fc3048aedf5" />

Esto lo que hizo fue que instalo 120 dependencias y se "auditaron" 121, lo que pueden ser las descargadas junto con el proyecto. Esto lo que hace es confirmar las librerias que se necesitan y guardarlas localmente para que el proyecto funcione y aparte de esto, la auditoria que realiza en el proyecto es como una forma de corroborar que no hayan vulnerabilidades para poder ejecutarlo, por eso la linea final.

Ya lo de la mitad, me puse a investigar y lo de los 17 packages es que estos mismos son de codigo abierto que buscan una financiación o donaciones.

### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?
Este fue el mensaje

<img width="831" height="102" alt="image" src="https://github.com/user-attachments/assets/c70ebc94-fb50-499b-8b96-9c9e2807cad2" />

Esto significa que el npm activo el script de inicio del proyecto, osea el server.js que pone en marcha un servidor web en este caso para poder que se vea lo que el proyecto tenga que ofrecer.

### Describe lo que ves inicialmente en page1 y page2 en tu navegador.

Cuando abri las paginas por primera vez, se veia un circulo rojo con un punto negro en el centro en cada una de las paginas.

<img width="2559" height="1389" alt="image" src="https://github.com/user-attachments/assets/555297b9-ba97-41bd-9cb0-99e3c89cfc31" />

ya despues cambia visualmente pero eso se explica mas adelante :d 

### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?

<img width="730" height="222" alt="image" src="https://github.com/user-attachments/assets/55db2559-db2f-46aa-8232-53b85031b37a" />

Estos mensajes indican la posición inicial de los dos circulos,tanto como su ancho y altura, ya cuando se queda quieto aparece el mensaje de que todos los clientes estan sincronizados.

### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

Si cambia visualmente, el punto negro cambia a ser un cable que conecta ambos circulos, sin importar que esten separados por las ventanas.

<img width="2499" height="1273" alt="image" src="https://github.com/user-attachments/assets/b3cf6c4e-ae6e-42a8-a54a-1467aa57732f" />

Aunque si ponemos una pagina sobre la otra, el circulo que esta abajo como que entra a la pagina que esta arriba.

<img width="2498" height="1272" alt="image" src="https://github.com/user-attachments/assets/ae0a6cec-629d-453d-b879-f701b4151d7e" />

En cuanto a la consola del navegador aparecen estos mensajes:

<img width="539" height="1087" alt="image" src="https://github.com/user-attachments/assets/0f78f144-84ce-44b3-923c-b9000131f03a" />

y en el caso de la consola de la terminal, aparece el mismo mensaje que en el punto anterior, solo que cambia constantemente mientras movemos las ventanas porque actualiza la posicion en la que los circulos, osea, asi:

<img width="767" height="754" alt="image" src="https://github.com/user-attachments/assets/8a9d4159-f05d-4a26-95bb-ac76cb39f3a6" />

Ya cuando lo dejo quieto aparece que todos los clientes estan sincronizados.

## ACTIVIDAD 02

### Piensa en cómo te conectas a Internet en casa o en la Universidad. ¿Usas Wi-Fi? ¿Un cable de red? Eso es simplemente tu “rampa de acceso” a la gran red de carreteras. ¿Qué pasaría si esa rampa se corta? Anota tus ideas.

Normalmente en mi casa cuando se trata del computador uso cable de red, pero ya con los dispositivos inalambricos si uso Wi-Fi. Lo mismo en la universidad, los pcs que usamos tienen cable de red mientras que los dispositivos inalambricos toca conectarlos a upbwifi. Ahora, si digamos que la rampa de acceso se rompe y tengo cable de red se corta, si el pc tiene lo que le permite conectar al Wi-Fi y ya se ha conectado antes, pasa a la red wifi. Si rompemos la rampa de acceso del Wi-Fi, ahi si nos quedamos sin internet en el que navegar porque saldriamos de esta gran red de carreteras por un camino en el cual no hay nada en lo que podamos navegar.

Entonces:

- Si tengo cable de red y en el pc se puede usar Wi-Fi, cuando se corta la rampa del cable pasa a Wi-Fi
- Si se daña la Rampa del Wi-Fi, ya no estaremos en la gran red de carreteras y iremos por un camino en el cual no hay algo en lo que podamos "navegar"

### ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

Si pedimos un taxi, nosostros le pedimos al conductor que nos lleve a un lugar y por ende el responde dejandonos donde le indicamos, si quiero ver algo en alguna plataforma como youtube o algo asi, navego o busco algo que me guste y cuando lo encuentre, le pido al servidor que me entregue lo que quiero ver, como un video o una serie. En el caso del restaurante, nosotros seriamos el cliente y ellos el servidor, donde nosotros pedimos la comida y ellos nos la entregan.

Siempre tiene que estar esa relacion donde el cliente es el que pide y el servidor el que entrega lo que pedimos, como en el navegador donde nosotros buscamos algo y el servidor nos da millones de resultados para lo que estanmos buscando.

### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

A mi me gusta mucho YouTube.

 https://www.youtube.com
 
Donde este tiene el https y el nombre de dominio que seria www.youtube.com. Ahora, si me meto a un video se le agrega a la URL la ruta, como esto:

https://www.youtube.com/watch?v=ZotF4A7uThc&t=12s

Donde el watch y esos numeros representan el codigo del video que estoy viendo. En youtube cada video tiene su codigo propio con la URL. Ahora, si escribo el nombre del dominio me lleva a la pagina principal de youtube, osea el inicio donde te aparecen videos de temas que te gustan.

<img width="2519" height="1348" alt="image" src="https://github.com/user-attachments/assets/95a60858-2e80-4803-882e-a68c228d88a2" />

### COMPARACION ENTRE HTTP, ASCII Y BINARIO CON FRAMING.

#### SIMILITUDES ENTRE ESTOS

- Todos necesitan una forma donde el receptor tiene que entender de como inicia y termina el mensaje
- Tienen un formato acordado, el receptor tiene que entenderlo todo porque tienen la misma convención
- Funcionan si ambos lados usan el mismo idioma
- En los protocoles seriales es comando -> respuesta, en http es cliente -> servidor, similares en este aspecto

#### DIFERENCIAS

- El nivel de abstraccion, mientras que los protocolos trabajan con bytes; el http se monta sobre TCP/IP.
- El formato de los datos, los protocolos tienen un formato mas facil (Textos simples o compactos), mientras que el http mezcla encabezados y datos binarios haciendolo un poco mas dificil.
- A diferencia con la aplicacion del framing en los protocolos, en el http hay varios mecanismos como líneas de inicio, headers clave-valor, content-length, etc.
- Los protocolos son mas para dispositivos, mientras que el http esta mas relacionado a escalar en internet, interoperar entre miles de clientes y servidores distintos, y soportar extensiones.

#### ¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?

HTTP tiene que ser más complejo que solo mandar bytes como hacía con el micro:bit porque no es solo para conectar dos aparatos, sino para que muchísimos dispositivos diferentes en todo el mundo se entiendan entre sí. En el micro:bit me basta con mandar un número o un texto y ya, pero en Internet se necesita decir qué quiero pedir, de dónde, en qué formato, si necesito seguridad, y que además funcione igual sin importar si lo uso desde un celular, un computador o un servidor. Por eso HTTP tiene reglas más largas, con encabezados y códigos, para que todo quede claro y no haya errores al comunicarse.

### ACTIVIDAD SOBRE LA PAGINA WEB SIMPLE

#### ¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?
La que define la estructura basica de la pagina, Sin HTML no habría donde escribir ni un botón que pulsar y en el caso de un formulario de login, serían los campos de texto para escribir el nombre de usuario y la contraseña, el botón de "Iniciar sesión", los titulos o etiquetas que indican que debe ir en cada campo.

#### ¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?
Se encarga de como se ve la pagina, puede darle color a los botones, cambiarle la tipografia, el tamaño, poner margenes, etc. En resumen permite que el formulario no solo funcione, sino que también sea mas atractivo y facil de usar.

#### ¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?
La logica y la interacción con el usuario, comprueba si los campos estan vacíos antes de enviar, valida que la contraseña tenga cierta cantidad de caracteres o que el correo tenga formato correcto. Tambien puede mostrar mensajes si el usuario se quivoca en algun dato y puede agregar mas funciones para tener una pagina mas completa.

### Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.
El bucle funciona como si fuera un reloj que no para, repite las instrucciones muchas veces por segundo. Asi, aunque nada cambie, el programa sigue dibujando la pantalla completa una y otra vez.

En cambio, el modelo de esperar a que algo pase y reaccionar es diferente. Aqui el programa se queda quieto hasta que ocurre un evento, por ejemplo cuando el usuario da clic, mueve el mouse o escribe en el teclado. En ese momento se ejecuta el codigo que corresponde.

#### ¿Qué ventajas crees que tiene el modelo basado en eventos para una interfaz de usuario web?
- Ahorra recursos, ya que el navegador no gasta energia del procesador ni de la bateria dibujando cosas que no cambiaron.
- Es mas rapido, porque solo se actualiza lo que de verdad necesita cambiar.
- Es mas facil, ya que solo hay que escribir lo que debe ocurrir cuando el usuario hace una acción.

#### ¿Sería eficiente tener un bucle draw() redibujando toda la página 60 veces por segundo si nada ha cambiado?
Si tuviéramos un draw redibujando toda la página 60 veces por segundo sin que nada cambie, sería muy ineficiente ya que la computadora se cansaria rapido, gastaria bateria, y la página se pondría lenta. Por eso, para páginas web es mucho mejor usar el modelo de eventos que solo reacciona cuando algo pasa.

### ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?
Es mas util porque permite trabajar con un solo lenguaje en todo el proyecto, lo que hace más facil aprenderlo, mantener el código y evitar repetir funciones como validaciones. Aparte, los desarrolladores pueden aprovechar la gran cantidad de bibliotecas que hay por la web, y tambien pueden compartir partes del programa entre cliente y el servidor, ya no se me ocurre nada mas.

### Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?

Lo que diferencia el HTTP es que funciona con un modelo de cliente - servicio, donde digamos que un cliente al usar un navegador siempre tiene que pedirle algo al servidor, y el servidor tiene que responder esas peticiones. Mientras que el WebSockets/socket.io establece una conexión mas continua entre cliente y servidor, que permite enviar y recibir datos en tiempo real sin necesidad de pedirlo a cada rato. Este tipo se usa en aplicaciones donde la actualización es importante como no se, un chat online, juegos multificador, directos, colaboraciones en documentos como lo pueden ser canva o tambien gps.

## ACTIVIDAD 03

### EXPERIMENTO #1

Aca se cambio la primera ruta en el codigo de server.js de page1 a pagina_uno

#### Intenta acceder a http://localhost:3000/page1. ¿Funciona?

No no funciona, debido a que aunque en todo el codigo aparezca page1, al modificarlo le estamos pidiendo que abra esta pagina con pagina_uno.

<img width="1915" height="601" alt="image" src="https://github.com/user-attachments/assets/c076a141-1aec-41a2-980a-19c4455e6805" />

#### Ahora intenta acceder a http://localhost:3000/pagina_uno. ¿Funciona?

Esta si funciona por la modificación que hicimos.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/7b0ca750-199c-4322-8a5e-a3845a0500b1" />

#### ¿Qué te dice esto sobre cómo el servidor asocia URLs con respuestas? 

En el codigo hay un req y un res, yo entiendo que son requerimiento y respuesta. Por eso cuando cambiamos lo del app.get a pagina_uno

```js
app.get('/pagina_uno', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});
```
Le estamos pidiendo al server que nos lleve a page1, solo que el nombre de acceso a este es con pagina_uno.

### EXPERIMENTO #2

#### Abre http://localhost:3000/page1 en una pestaña. Observa la terminal del servidor. ¿Qué mensaje ves? Anota el ID.

A user connected - ID: iz_HVFUvb0hzS4OTAAAF

#### Abre http://localhost:3000/page2 en OTRA pestaña. Observa la terminal. ¿Qué mensaje ves? ¿El ID es diferente?
Si el id es diferente.
A user connected - ID: 4O2nCIAXXEnBXe-fAAAH

#### Cierra la pestaña de page1. Observa la terminal. ¿Qué mensaje ves? ¿Coincide el ID con el que anotaste?
Si, es el mismo id que anote al principio
User disconnected - ID: iz_HVFUvb0hzS4OTAAAF

#### Cierra la pestaña de page2. Observa la terminal.
Si, pasa lo mismo si cierro la page2, me suelta el mismo id.
user disconnected - ID: 4O2nCIAXXEnBXe-fAAAH

### EXPERIMENTO #3

#### Mueve la ventana de page1. Observa la terminal del servidor. ¿Qué evento se registra (win1update o win2update)? ¿Qué datos (Data:) ves?
Se registra eñ win1update, y estos son los datos.
Received win1update from ID: iTP2yCkegHuLkeEpAAAJ Data: { x: 268, y: 119, width: 1572, height: 914 }

#### Mueve la ventana de page2. Observa la terminal. ¿Qué evento se registra ahora? ¿Qué datos ves?
Ahora sale el win2update, y esto son los datos
Received win2update from ID: abxEj6i33DGM7HZNAAAH Data: { x: 233, y: 55, width: 1572, height: 914 }

#### Experimento clave: cambia socket.broadcast.emit(‘getdata’, page1); por socket.emit(‘getdata’, page1); (quitando broadcast). Reinicia el servidor, abre ambas páginas. Mueve page1. ¿Se actualiza la visualización en page2? ¿Por qué sí o por qué no? (Pista: ¿A quién le envía el mensaje socket.emit?). Restaura el código a broadcast.emit.

<img width="1858" height="1020" alt="image" src="https://github.com/user-attachments/assets/869fbf14-0caa-4fd8-80e3-33536560612f" />
Yo creo que antes la que no se actualiza es la del page1, porque al mover el page2, esta misma si se actualiza y se ve como subo la pagina, el cable se mueve al del circulo de la page1, pero si hago lo contrario, la page1 como que se intenta mover pero no deja, mas o menos como se ve en la imagen que puse. Basicamente, al modificarlo el socket.emit envia los datos a win1update, osea que se envia al mismo cliente que lo emitio, mientras que en el caso de la page2, con el broadcast se envia a todos clientes menos el que lo emitio (win2update).

### EXPERIMENTO #4
#### inicia el servidor. ¿Qué mensaje ves en la consola? ¿En qué puerto dice que está escuchando?
Esta escuchando al puerto 3001
Server is listening on http://localhost:3001

#### Intenta abrir http://localhost:3000/page1. ¿Funciona?
noup
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/6148d7c7-361b-442b-8f4b-8f2194bd8732" />

#### Intenta abrir http://localhost:3001/page1. ¿Funciona?
sip
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/61753f48-687f-4050-88bf-8538e4f93cb3" />

#### ¿Qué aprendiste sobre la variable port y la función listen? Restaura el puerto a 3000.
Que al cambiar el numero del port, este va a escuchar a este numero con el listen, osea, si aparece 3001 en el port, el localhost tiene que aparecer con el 3001 porque si no, no lleva a ningun lado.

## ACTIVIDAD 04

### EXPERIMENTO #1

#### Abre la consola de desarrollador (F12).
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/da675eff-a681-4ac6-aee7-0ae719fb7b7a" />

#### Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica?
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/87316741-6b9e-4bea-a4f8-dab7b3587d89" />

Si hay un error, esto lo que indica es que al tener el server cerrado, no se puede acceder a esta pagina hasta que lo iniciemos

<img width="520" height="177" alt="image" src="https://github.com/user-attachments/assets/4ea51eae-3de4-4710-bf04-95749155ea90" />

#### Vuelve a iniciar el servidor y refresca la página. ¿Desaparecen los errores?
sip
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/5818d47f-0cfc-4fb9-8922-eda240fee54c" />

### EXPERIMENTO #2

<img width="1917" height="995" alt="image" src="https://github.com/user-attachments/assets/8e94af3f-7921-4c2e-a9fa-3f82f713ad05" />


<img width="1919" height="991" alt="image" src="https://github.com/user-attachments/assets/ebd6debc-e83f-4836-9f2c-10d28d68cf65" />

Al comentar la función del listener connect, la page2 se queda esperando la conexión de la otra ventana, pero como esta funcion que comentamos es la encargada de eso la page2 se va aquedar esperando la conexión con la otra ventana para siempre.

### EXPERIMENTO #3

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/dc84d7d3-f8bc-4cf0-8deb-006ff16b3631" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/bd0db505-2565-4645-a244-1b3621a5fd47" />

Pues no me paso nada raro, al mover una pagina se envian los datos de donde se mueven o donde se ubican a la otra, esto es para sincronizarlos y poder generar el cable.

### EXPERIMENTO #4

```js

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (
        currentPageData.x !== previousPageData.x || 
        currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || 
        currentPageData.height !== previousPageData.height
    ) {
        console.log('Cambio detectado en posición o tamaño de la ventana');

        point2 = [currentPageData.width / 2, currentPageData.height / 2];
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}
```

<img width="1181" height="1040" alt="image" src="https://github.com/user-attachments/assets/4f249b0e-058e-4426-861f-b0e936ad6561" />

El mensaje "Cambio detectado en posición o tamaño de la ventana" se repite muchas veces porque el código no está comparando bien los datos antiguos con los nuevos. En vez de copiar los valores de la ventana, está copiando la referencia, o sea, los dos objetos (previousPageData y currentPageData) terminan siendo el mismo. Entonces, aunque parezca que está comparando, en realidad siempre se ven iguales o cambian juntos. Para arreglarlo, hay que hacer una copia real usando previousPageData = { ...currentPageData };, así sí se guardan los valores anteriores y la comparación funciona como debe.

### EXPERIMENTO #5

https://github.com/user-attachments/assets/10d15862-ae51-4ef5-b5cd-bc1e2b4f3e73

Para innovación creativa, lo que hice fue que cada vez que alejemos la ventana de la otra, el circulo de la pagina 2 se vuelva mas pequeño, mientras que si lo acercamos, se vuelve mas grande. Esto se logra modificando la function draw del codigo hacia abajo:

```js
function draw() {
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    let distancia = resultingVector.mag();

   
    background(map(distancia, 0, 1000, 255, 0));  
    
    if (!isConnected) {
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    
    let dynamicSize = map(distancia, 0, 1000, 200, 50); 
    drawCircle(point2[0], point2[1], dynamicSize);

    checkWindowPosition();

    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, 
               resultingVector.y + remotePageData.height / 2, 
               150);
    line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();
  
    fill(0, 0, 0, 150); 
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, 1*height / 6, textW, textH, 10);
   
    fill(statusColor);
    text(message, width / 2, 1*height / 6);
}

function drawCircle(x, y, size = 150) {
    fill(255, 0, 0);
    ellipse(x, y, size, size);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```

## ACTIVIDAD 05

### EXPLICACION DE LA IDEA Y BOCETO

Como tal, la idea es hacer una especie de piano tiles, sin musica obviamente, donde desde la page1 se generen las tiles negras y pasen a la page2 donde uno tenga que presionar las teclas D F K L, si aparecen con un rojo mas oscuro es que fallo al no presionar la tecla a tiempo perfecto, pero si aparece un color verde al presionar la tecla significa que si fue presionada con un timing perfecto. Es algo simple pero interesante

<img width="2559" height="1231" alt="image" src="https://github.com/user-attachments/assets/27584fb6-251e-4d47-810b-d90c0d6a032e" />

<img width="2559" height="1226" alt="image" src="https://github.com/user-attachments/assets/f3997a8d-5e35-4b92-b123-b11c09d1bea1" />

### IMPLEMENTACIÓN DE LA IDEA

https://github.com/user-attachments/assets/5c4d8829-aec4-415b-b6f2-1f9560ba4a33

no supe arreglar porque las teclas al pasar de pagina se mueven mas rapido pero por lo menos es funcional :D
y tambien implementar musica era mas dificil asi que por eso no lo hice. 

### CODIGOS

#### SERVER.JS

```js
const express = require("express");
const http = require("http");
const socketIO = require("socket.io");
const path = require("path");
const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;


let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };

let connectedClients = new Map();
let syncedClients = new Set();


app.use(express.static(path.join(__dirname, "views")));

app.get("/page1", (req, res) => {
  res.sendFile(path.join(__dirname, "views", "page1.html"));
});

app.get("/page2", (req, res) => {
  res.sendFile(path.join(__dirname, "views", "page2.html"));
});


io.on("connection", (socket) => {
  console.log("Cliente conectado - ID:", socket.id);
  connectedClients.set(socket.id, { page: null, synced: false });


  socket.on("disconnect", () => {
    console.log("Cliente desconectado - ID:", socket.id);
    connectedClients.delete(socket.id);
    syncedClients.delete(socket.id);
    socket.broadcast.emit("peerDisconnected");
  });

 
  socket.on("tilePosition", (data) => {
    console.log("tilePosition recibido:", data);
    if (isValidTileData(data)) {
      io.emit("updateTile", data);
    }
  });

  
  socket.on("newTile", (tile) => {
    console.log("Nueva tile recibida de page1:", tile);
    if (tile && typeof tile.x === "number" && typeof tile.y === "number") {
      socket.broadcast.emit("newTile", tile);
    }
  });

 
  socket.on("keyPress", (data) => {
    console.log("keyPress recibido:", data);
    io.emit("keyResult", data);
  });


  socket.on("win1update", (window1) => {
    console.log("win1update de", socket.id, window1);
    if (isValidWindowData(window1)) {
      page1 = window1;
      connectedClients.set(socket.id, { page: "page1", synced: false });
      socket.broadcast.emit("getdata", { data: page1, from: "page1" });
      checkAndNotifySyncStatus();
    }
  });

  socket.on("win2update", (window2) => {
    console.log("win2update de", socket.id, window2);
    if (isValidWindowData(window2)) {
      page2 = window2;
      connectedClients.set(socket.id, { page: "page2", synced: false });
      socket.broadcast.emit("getdata", { data: page2, from: "page2" });
      checkAndNotifySyncStatus();
    }
  });

  socket.on("requestSync", () => {
    const clientInfo = connectedClients.get(socket.id);
    if (clientInfo?.page === "page1") {
      socket.emit("getdata", { data: page2, from: "page2" });
    } else if (clientInfo?.page === "page2") {
      socket.emit("getdata", { data: page1, from: "page1" });
    }
  });

  socket.on("confirmSync", () => {
    syncedClients.add(socket.id);
    const clientInfo = connectedClients.get(socket.id);
    if (clientInfo) {
      connectedClients.set(socket.id, { ...clientInfo, synced: true });
    }
    checkAndNotifySyncStatus();
  });
});


function isValidWindowData(data) {
  return (
    data &&
    typeof data.x === "number" &&
    typeof data.y === "number" &&
    typeof data.width === "number" &&
    data.width > 0 &&
    typeof data.height === "number" &&
    data.height > 0
  );
}

function isValidTileData(data) {
  return (
    data &&
    typeof data.id === "string" &&
    typeof data.x === "number" &&
    typeof data.y === "number"
  );
}


function checkAndNotifySyncStatus() {
  const page1Clients = Array.from(connectedClients.values()).filter(
    (info) => info.page === "page1"
  );
  const page2Clients = Array.from(connectedClients.values()).filter(
    (info) => info.page === "page2"
  );

  const bothPagesConnected =
    page1Clients.length > 0 && page2Clients.length > 0;
  const allClientsSynced = Array.from(connectedClients.keys()).every((id) =>
    syncedClients.has(id)
  );
  const hasMinimumClients = connectedClients.size >= 2;

  console.log(
    `Debug - Clients: ${connectedClients.size}, P1: ${page1Clients.length}, P2: ${page2Clients.length}, Synced: ${syncedClients.size}`
  );

  if (bothPagesConnected && allClientsSynced && hasMinimumClients) {
    io.emit("fullySynced", true);
    console.log("Todos los clientes están sincronizados");
  } else {
    io.emit("fullySynced", false);
    console.log(
      `Sync status: pages=${bothPagesConnected}, synced=${allClientsSynced}, clients=${connectedClients.size}`
    );
  }
}

server.listen(port, () => {
  console.log(`Servidor corriendo en http://localhost:${port}`);
});
```
#### page1.js

```js
let socket;
let isConnected = false;
let tiles = [];
let cols = 4;
let tileSize = 80;
let keys = ["D", "F", "K", "L"];

let tileInterval;

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);

    socket = io();

    
    socket.on("connect", () => {
        console.log("Conectado con ID:", socket.id);
        isConnected = true;
    });

    socket.on("disconnect", () => {
        console.log("Desconectado del servidor");
        isConnected = false;
    });

   
    tileInterval = setInterval(() => {
        let col = floor(random(cols));
        let rectHeight = height / cols;
        let y = rectHeight * col + rectHeight / 2 - tileSize / 2;

        let tile = {
            id: Date.now() + "-" + col,
            col: col,
            x: 0,
            y: y,
            speed: 5,
            remove: false
        };

        tiles.push(tile);
    }, 1500);
}


function draw() {
    background(220);

    if (!isConnected) {
        showStatus("Conectando al servidor...", color(255, 165, 0));
        return;
    }

    for (let t of tiles) {
        t.x += t.speed;

        fill(0);
        rect(t.x, t.y, tileSize, tileSize);

        if (t.x >= width) {
            socket.emit("tilePosition", {
                id: t.id,
                col: t.col,
                x: 0,           
                y: t.y / height 
            });
            t.remove = true;
        }
    }

    
    tiles = tiles.filter(t => !t.remove);
}


function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();

    
    fill(0, 0, 0, 150);
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, height / 6, textW, textH, 10);

    
    fill(statusColor);
    text(message, width / 2, height / 6);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}
```
#### page2.js

```js
let socket;
let tiles = [];
let cols = 4;
let tileSize = 80; 
let keys = ["D", "F", "K", "L"];
let keyMap = { "d": 0, "f": 1, "k": 2, "l": 3 };
let columnColors = ["#ff6666", "#ff6666", "#ff6666", "#ff6666"];
let feedbackTimer = [0, 0, 0, 0];

function setup() {
  createCanvas(windowWidth, windowHeight);
  frameRate(60);

  socket = io();

  socket.on("updateTile", (data) => {
    if (!isValidTileData(data)) return;

    let rectHeight = height / cols;
    let y = rectHeight * data.col + rectHeight / 2 - tileSize / 2;

    tiles.push({
      id: data.id,
      col: data.col,
      x: data.x * width,   
      y: y,
      hit: false,
      speed: 8
    });
  });

  socket.on("keyResult", (data) => {
    if (data && typeof data.col === "number") {
      columnColors[data.col] = data.success ? "#00cc66" : "#cc0000";
      feedbackTimer[data.col] = 30;
    }
  });
}

function draw() {
  background(240);

  let rectHeight = height / cols;

  for (let i = 0; i < cols; i++) {
    if (feedbackTimer[i] > 0) {
      feedbackTimer[i]--;
      if (feedbackTimer[i] === 0) columnColors[i] = "#ff6666";
    }

    fill(columnColors[i]);
    rect(width - 120, rectHeight * i, 120, rectHeight);

    fill(0);
    textAlign(CENTER, CENTER);
    textSize(24);
    text(keys[i], width - 60, rectHeight * i + rectHeight / 2);
  }

  for (let t of tiles) {
    if (!t.hit) t.x += t.speed;

    fill(0);
    rect(t.x, t.y, tileSize, tileSize);

    if (t.x > width - 120 && !t.hit) {
      columnColors[t.col] = "#cc0000";
      feedbackTimer[t.col] = 30;
      t.hit = true;
      socket.emit("keyPress", { col: t.col, success: false });
    }
  }

  tiles = tiles.filter(t => !t.hit && t.x < width + tileSize);
}

function keyPressed() {
  let col = keyMap[key.toLowerCase()];
  if (col !== undefined) {
    let hitTile = tiles.find(
      t => !t.hit && t.col === col && t.x > width - 140 && t.x < width - 100
    );

    if (hitTile) {
      hitTile.hit = true;
      socket.emit("keyPress", { col: col, success: true });
    } else {
      socket.emit("keyPress", { col: col, success: false });
    }
  }
}

function isValidTileData(data) {
  return (
    data &&
    typeof data.x === "number" &&
    typeof data.col === "number"
  );
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

```
Ya esto fue todo lo que cambie con respecto al original:d 

## AUTOEVALUACIÓN

### ACTIVIDAD 1 (5)

Como primera actividad para conocer esta nueva forma de hacer las cosas, siento que me fue bastante bien haciendo las actividades y aparte iba conociendo como funcionan cosas como el git bash ya que en mi caso nunca lo usaba (solo github desktop), y esto nuevo del node.js para hacer funcionar un servidor en linea, pero como tal la actividad esta completa, con cosas que fui descubriendo mediante las hacia y otras que investigue orque me surgieron la duda. Por eso al ser esta actividad tan corta esta fue mi defensa de porque creo que me merezco el 5.

### ACTIVIDAD 2 (5)

Esta parte era mas teorica o de pensar por uno mismo, donde no solo investigue sino que tambien aporte con los conocimientos que ya tenia y respondi esas preguntas mas situacionales como por ejemplo la del cliente-servidor, que me hizo entender mas como funciona esto al usar el ejemplo del restaurante, tambien comprendi muy bien lo de la url y tambien sus partes como el http, su dominio publico y las posibles paginas que se pueden encontrar al final del link. Donde siento que respondi de manera correcta a estas preguntas y di evidencias de que busque como hacerlas, como por ejemplo la actividad de la pagina web que me gusta o algo asi.

Ya llegando a la fase final de esta actividad que estaba mas relacionado a la parte mas teorica de los http, la verdad es que siento que los conceptos me quedaron claros al realizar estas actividades donde si me toco buscar porque no tenia tanto conocimiento para responder por ejemplo lo del envio de bytes en comparacion al microbit, y me quedo claro que es porque el microbit se centra en enviar entre dos dispositivos o los que tenga conectados, mientras que en http tienden a ser cientos de miles dependiendo de lo que se quiera hacer ya que funciona diferente, por ejemplo un navegador web debe tener trillones de envios en poco tiempo por todos los dispositivos que lo usan, y tambien mencionar la pregunta final que me toco buscar sobre los websockets/socket.io porque como tal no lo conocia, pero ahora me queda claro que usar esto es mejor que el httpp.

Siento que respondi de manera completa a todas las preguntas y me di el tiempo de comprender las preguntas que se me hacian para buscarle una respuesta, asi que creo que me merezco el 5 por eso.

### ACTIVIDAD 3 (5)

Esta actividad como tal me hizo ver el funcionamiento de lo que ya habiamos visto en las anteriores actividades pero ya aplicado en un codigo,ene ste caso en el server.js, y siento que estos experimentos estuvieron sencillos, aunque hubo otro que alguno que si me puso a pensar mas, pero como tal de esto saque como puede funcionar el servidor al modificar cosas como lo de la pagina_uno, los mensajes de la consola, el port y el listen.

Pero como tal, al ser una actividad de experimentación era mas para ver el funcionamiento que podria ayudar para la actividad 5, y al ser tambien experimentos bastante cortos de hacer, junto a que siento que respondi bien y subi evidencias de que efectivamente hice los experimentos, siento que si me merezco el 5.

### ACTIVIDAD 4 (5)

Pasa casi lo mismo que con lo anterior, solo que en esta explore por dentro el funcionamiento de las paginas y me dejo claro que de ahi es donde se hace la parte visual, no en el html como yo creia al principio. Pero como tal, al tener que experimentar solo con la page2.js y teniendo en cuenta que el codigo era igual al de la page1.js, de aca tambien saque cosas para poder hacer la actividad 5 aunque si me quedo mas diferente a este ejemplo, pero como tal, la actividad esta completa y los experimentos estan evidenciados, siento que con eso ya merezco el 5.

### ACTIVIDAD 5 (5)

En esta actividad aplique lo que vimos en las actividades pasadas, aunque tambien sinceramente le pregunte a la ia como podria hacer esta actividad ya que en el ejemplo que se dio para esta unidad, el page1.js y el page2.js eran lo mismo, aqui lo que quise hacer fue el piano tiles donde en la page1 se generan las tiles negras y en la page 2 se pudiera jugar como si fuera el juego de celular o un guitar hero, aunque si me quedo un poco dificil ya que si cuesta sacar la tecla verde. Pero como tal la actividad si esta completa y todo esta con su respuesta, por eso diria que merezco el 5.

Aunque si me hubiera gustado meterle una cancion que este sincronizada con las tiles negras para que fuera mas intuitivo, pero como creo que eso lo vamos a ver en las unidades que faltan siento que con esto cumpli, es una aplicacion interactiva en tiempo real, por lo que creo que la nota es merecida. Asi que como dice el dicho, siembra vacas para que coseches vacaneria :d 

<img width="201" height="251" alt="image" src="https://github.com/user-attachments/assets/695d5b8e-044d-4928-8606-33d9c8c27d66" />










































