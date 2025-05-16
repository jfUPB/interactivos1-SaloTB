## Análisis del servidor puente (server.js)

### ¿Cuál es la función principal de express.static(‘public’) en este servidor? ¿Cómo se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?
Se encarga de buscar un archivo como las URL y enviarlos directamente a el navegador que pidio el archivo, esto es mas facil de utilizar que lo usado en la unidad 6 donde para cada archivo HTML se necesitaba una ruta separada.

### Explica detalladamente el flujo de un mensaje táctil: ¿Qué evento lo envía desde el móvil? ¿Qué evento lo recibe el servidor? ¿Qué hace el servidor con él? ¿Qué evento lo envía el servidor al escritorio? ¿Por qué se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
cada vez que se establece una coneccion websoket ya sea por parte del escritorio o el movil se utiliza io.on(‘connection’, (socket) => { … }); que es la base de la funcion socket.io (Cada cliente conectado tiene su objeto tipó socket), luego de esto se realiza el envio de un "mesaage" un evento
que contiene los cambios que sucedieron en este objeto soket. Estos datos se kmuestran en console.log(), finalmente se tiene la retrasmicion que implementa el bortcast que envia la informacion a todos los clientes conecatdos menos al que envio los datos.

### Si conectaras dos computadores de escritorio y un móvil a este servidor, y movieras el dedo en el móvil, ¿Quién recibiría el mensaje retransmitido por el servidor? ¿Por qué?
Lo resiviria el segundo movil y el escritorio gracias a broadcast que envie a los clientes conectados el mensjae menos al mismo que los envio.

### ¿Qué información útil te proporcionan los mensajes console.log en el servidor durante la ejecución?
Console:log muestra los datos enviados en tiempo real y ademas quien los envio lo que es muy importante en especial si tienes mas de dos dispositivos conectados 
