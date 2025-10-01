
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




















