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
Esto es lo que se puede ver en la consola:

    Connected to serial port 
    A pressed 
    microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
     
    Microbit ready to draw 
    92
    microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 
     
    microBitX: 500 microBitY: 500 microBitAState: false microBitBState: false 
     
    204
    microBitX: 256 microBitY: 500 microBitAState: false microBitBState: false 

El error puede ser causado por que estan llegando menos o mas bytes de los esperados que en este caso son 6. Como el codigo esta esperando grupos o paquetes de datos organizados y no los esta resiviedo puede estar causando este error. Ademas este desorden en los datos puede deberse a que no hay un limite establecido entre el final e incio de los paquetes, por lo que el codigo no los interpreta como queremos que lo haga
 
## Analiza el código, observa los cambios. Ejecuta y luego observa la consola. ¿Qué ves?
Esto es lo que se ve en la consola:

    Connected to serial port 
    Microbit ready to draw 
    A pressed 
    75
    microBitX: 500 microBitY: 524 microBitAState: true microBitBState: false 

 Ahora se esta ejecutando correctamente pues los paquetes de bytes se ordenan y procesan gracias a la funcion "function readSerialData()" 

## ¿Qué cambios tienen los programas y ¿Qué puedes observar en la consola del editor de p5.js?

Esto es lo que se puede ver en la consola: 

    Connected to serial port 
    Microbit ready to draw 
    A pressed 
    B released 
    A pressed 

Estos son los principales cambios del codigo: 

    // Si el paquete es válido, extrae los valores
    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + windowWidth / 2; //Se agrega para la direccion del micro:bit 
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

Para el uso de los botones del microbit y su posicion a la hora de dibujar en la consola de p5.js se cambia:

    xValue = 500
       yValue = 524
       aState = True
       bState = False

por:

    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
