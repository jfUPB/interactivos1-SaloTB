## Consolidación de lo aprendido

En la unidad anterior abordaste la construcción de un protocolo ASCII. En esta unidad realizaste lo propio con un protocolo binario. Realiza una tabla donde compares, 
según la aplicación que modificaste en la fase de aplicación de ambas unidades, los siguientes aspectos: eficiencia, velocidad, facilidad, usos de recursos. Justifica con 
ejemplos concretos tomados de las aplicaciones modificadas.

![image](https://github.com/user-attachments/assets/cf64fa79-07ae-423c-b7ec-67917ee52f1f)

¿Por qué fue necesario introducir framing en el protocolo binario?
por qu elos datos binarios no tienen separadores visibles y el farming ayuda a delimitar los paquetes de datos

¿Cómo funciona el framing?
se utiliza un bte especial al incio que incique el incio de un nuevo paquete, luego se cuenta una catidad fija de bytes y asi se puede
saber el incio y el fin de cada paquete de bytes evitando datos corruptos 

¿Qué es un carácter de sincronización?
Uno de los caracteres especiales que permite marcar le incio de un paquete y evitar valores eeroneos sienod leidos

¿Qué es el checksum y para qué sirve?
es un valor que sivre para verificar los resumenes de los datos y que no haya errores en la transmision de los mismos

En la función readSerialData() del programa en p5.js:
¿Qué hace la función concat? ¿Por qué?

    function readSerialData() {
        let available = port.availableBytes();
        if (available > 0) {
            let newData = port.readBytes(available);
            serialBuffer = serialBuffer.concat(newData);
        }

une los bytes nuevos para formar un flujo continuo de datos 

En la función readSerialData() tenemos un bucle que recorre el buffer solo si este tiene 8 o más bytes ¿Por qué?

    while (serialBuffer.length >= 8) {
      if (serialBuffer[0] !== 0xaa) {
        serialBuffer.shift();
        continue;
      }

por que ne este portocolo el paquete valido son 8 bytes (1 header + 6 datos + 1 checksum) si hay menos no estaria el paquete completo y no 
se podria procesar

En el código anterior qué significa 0xaa?
Es el byte "especial" el que permite el farming

En el código anterior qué hace la función shift y la instrucción continue? ¿Por qué?
Shift elimina el primer byte para buscar el "especial" y conitnuo hace que bucle siga sin procesar los datos que siguen si no son un paquete valido

Si hay menos de 8 bytes qué hace la instrucción break? ¿Por qué?

    if (serialBuffer.length < 8) break;
detiene le bucle porque no hay suficientes datos para los 8 bytes osea el paquete 

¿Cuál es la diferencia entre slice y splice? ¿Por qué se usa splice justo después de slice?

    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8);

slice copia los primeros 8 bytes para analizarlos sin modificar ell buffer mientras que splice los elimina para no volverlos a procesar otra vez

A la siguiente parte del código se le conoce como programación funcional ¿Cómo opera la función reduce?

    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

suma todos los bytes del baquete para establecer el cheksum 

¿Por qué se compara el checksum enviado con el calculado? ¿Para qué sirve esto?

    if (computedChecksum !== receivedChecksum) {
        console.log("Checksum error in packet");
        continue;
    }
para detectar is hay errores en la transmicion de datos

En el código anterior qué hace la instrucción continue? ¿Por qué?
ignora el paquete actual si el cheksu no es el correto

¿Qué es un DataView? ¿Para qué se usa?

    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
sirve para leer los valores e interpretar los daros binarios de forma correcta

¿Por qué es necesario hacer estas conversiones y no simplemente se toman tal cual los datos del buffer?

    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;

por que los binarios se representa con bytes pero no se pueden leer directamente por lo que los cambia para interpretarlos ocmo numeros 
o signos segun necesite
