## Consolidación de lo aprendido

¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Es uan forma de comonuciacion de establece el como se deben de enviar los mensajes para la comunicacion entre dispositivos, aseguroa que todos los 
dispositivos enteindan los datos enviados de la msima manera

¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Es una forma facil de determinar los difernetes valores, los separa de forma organizada para que la cadena de texto pueda ser leida

¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Permite identificar la programa donde termina el mensaje

¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
por que permite organizar el flujo del programa dependiendo del estado actual del mismo, ademas hace al codigo mucho mas claro
y facil de manejar

¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
con comas y con un salto de linea al final

¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
significa que los numeros y caracteres se envian como texto legible

¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
porque se pueden obtener valores vacios o incompletos

¿Qué pasa si esto no se hace?

    if (port.availableBytes() > 0) {
        let data = port.readUntil("\n");
el programa podria leer datos "basura2 y esto podria probocar problemas en el codigo

¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
usando .trim() que elimina lso espacios en blanco saltos en linea y retronos

Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
usaria .split(" ") que divide la cadena de un arreglo en partes

Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
porque los datos del puerto serial llegan como texto por lo que deben ser convertidos despues en int() si son numero spor ejemplo

Si el micro:bit tiene los siguientes datos xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
Cada carácter es un byte en ASCII, por lo que se envían los siguientes bytes:
49 50 51 44 55 53 54 44 48 44 49 10 (44 es la coma y 10 el salto)
 
¿Qué aprendiste nuevo del micro:bit que no sabías antes?
Aprendi que cada una de sus acciones implica el envio de datos que pueden ser leidos e interpretados en diferentes "lenguajes"
 
¿Qué aprendiste nuevo de p5.js que no sabías antes?
Aprendi como leer datos desde un puerto serial en p5.js y como utilizar esa informacion para controlar proyectos como un caleidoscopio.
