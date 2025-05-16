## Describe con tus propias palabras cuál es la función del servidor Node.js en la arquitectura que exploramos. ¿Por qué los clientes p5.js no se comunican directamente entre sí?
Node.js actua como un intermediario entre la comunicacion de los clientes, esto lo hace resiviendo actualizaciones de estado y almacenando
ese estado en variables locales y luego envia esa informaicon a los demas clientes para mantener todo funcionando de forma rapida y presiza
Los clientes no se comunican entre si para evitar probelmas de seguridad o conexiones multiples entre ellos, ya que se tiene este servidor
que lo hace por ellos y lo maneja adecuadamente es mucho mas facil

## Explica la diferencia fundamental entre socket.emit() y socket.broadcast.emit() en el contexto de Socket.IO en el servidor ¿Cuándo usarías cada uno?
Socket.emit: Envia informaicon unicamente al cliente que origino la conexion, este se puede usar cuando se quiere enviar una respuesta 
personalizada a un cliente

Socke.brodcats.emit: Enia la informacion a todos los clientes menos al que envio el cambio de estado, este se puede usar cuando sequiere dar informacion
a todos los ya conectados menos al que origino la llamada como con las ventanas en los ejercisios

## Compara la comunicación mediante Node.js/Socket.IO con la comunicación serial
Node.js/Socket.IO: Utiliza Json y Binario para la comunicacion. Necesita una Red. Mejor para conectar navegadores o aplicaciones web.

comunicación serial: Utiliza ACCSI y Binario para la comunicacion. Necesita Farming y es mas suceptible a errores por ese metodo. Mejor para
controladores, sensores etc.

## ¿Qué rol juega el protocolo http y qué rol juega socket.io (que usa WebSockets por debajo) en la aplicación del caso de estudio?
http: Es el protocolo incial que conecta al cliente y al servidor cuando se conectan las paginas del ejercisio por primera vez

socket.io: Cuando la pagina ya esta conectada toma el control para habilitar la comunicacion en tiempo real entre el servidor y lso clientes
(Esto es lo que s ehace a traves de websocket) 

## ¿Qué fue lo más sorprendente o interesante que aprendiste sobre la comunicación en red en esta unidad?
Lo que mas me llamo la atencion fue coprender todo lo que sucede detras de la conexion en timepo real a la que estamos tan acotumbrados en nuestra vida diaria, no solo eso si no entender como esta coneccion no es tan directa como uno pensaria sino que tiene todos estos protocolos y conceptos como Node.js, socket.io y http que ayudan y realizan las conecciones, tambien me gusto aprender sobre los lenguajes que se necesitan para esta comunicacion y como estos influyen, pues nunca se me habia pasado por la cabeza que estos no fueran capaces de comunicarse por su idioma, al fin y al cabo todo son maquinas ¿no? eso solia pensar
