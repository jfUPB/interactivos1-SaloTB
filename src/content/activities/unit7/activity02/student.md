## Actividad 2 

### ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?
Dev tunels es un intermediario seguro entre una URL publica y el localhost (el dispositivo reseptor) (todo esto a traves de internet). Dev tunels reenvia la conexion de forma segura entre ambos dispositivos conecatdos por internet todo desde el servidor Node.js (tando de ida como de vuelta)

### ¿Por qué usamos JSON.stringify() en el emisor (móvil) y JSON.parse() en el receptor (escritorio)? ¿Qué problema resuelve JSON aquí?
Se utiliza JSON.stringify en el emisor pues se necesita que llegue al reseptor la informacion por medio de lineas de texto y no directamente como el objeto JavaScript, ya que estas cadenas de texto si se pueden enviar por la red, y en el receptor se covierte de nuevo en un objeto javascript
para que sea posible utilizarlo. El problema que resuelve aqui es el tipo de datos que se pueden o no enviar, los cambia para poder enviarlos entre ambos dispositivos y luego los cambia para que el reseptor pueda leer los datos enviados en forma de cadena de texto y lso interprete como la posicion

### Describe la función de touchMoved() y por qué se usa la variable threshold en el cliente móvil.
touchmoved es una funcion especifica que detecta el movimeinto de forma continua en mausex y maysey (opse ale movimeinto del dedo en la pantalla), sin emabrgo no envia constantemente la informacion recolectada, para esto se utiliza trheshold que se encarga de determinar dentro de un umbral de movimeinto
si el mismo fue lo suficientemente significativo para envial la señal de que se realizo un cambio o un movimienot y asi evitar saturar al receptor con informacionirrelevante

### ¿Qué otros eventos táctiles existen en p5.js y para qué tipo de interacciones podrían ser útiles (ej. un botón virtual, detectar un tap)?
Otros dos mencionados fueron touchstarted y touchended, para determinar cuando se comenzo a tocar la pantalla o cuando se dejo de tocar, tambien podria haber un detector de varios puntos de precion para reaqccionar a diferentes ocmandos, como en un videojuego donde se detecta el movimiento y el lanzamiento de
las habilidades, uno siendo un constante movimeinto en contacto con al pantalla y el otro siendo un tap

### Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?
Dev Tunels tiene acceso remoto desde cualquier lugar, sin cambios en el router ademas es escalable. Mientras tanto  el IP local es mas limitado como su nombre lo dice a la red local 

