# Caso de estudio: p5.js

En la unidad anterior se necesitaba hacer cambios de linea pues el grupo de datos no tenia un tamaño delimitado, en cambio en esta cituacion tenemos la delimitacion establecida a 6 bytes.

## Compara el código de la unidad anterior con este. ¿Qué cambios ves?

 El cambio mas notorio es el siguiente codigo para imprimir en la consola los valores del mismo micro:bit. Otro cambio notorio es que en esta parte del codigo ya no se esta trabajando con "True" y "False" como en la anterior y en cambio se trabaja con valores para determinar los estados. 
  
    if (port.availableBytes() >= 6) {
        let data = port.readBytes(6);
        if (data) {
          const buffer = new Uint8Array(data).buffer;
          const view = new DataView(buffer);
          microBitX = view.getInt16(0);
          microBitY = view.getInt16(2);
          microBitAState = view.getUint8(4) === 1;
          microBitBState = view.getUint8(5) === 1;
          updateButtonStates(microBitAState, microBitBState);

     print(`microBitX: ${microBitX} microBitY: ${microBitY} microBitAState: ${microBitAState} microBitBState: ${microBitBState} \n` );

    
## ¿Qué ves en la consola? ¿Por qué crees que se produce este error?

## Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?

## ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?
