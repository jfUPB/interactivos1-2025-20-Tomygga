
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

### EXPIREMENTO #3

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

























