# Repasa el caso de estudio

## Describe cómo se están comunicando el micro:bit y el sketch de p5.js. ¿Qué datos envía el micro:bit?
Se comunican a traves de puerto serial (UART) usando p5.webserial, p5.js accede al puerto serial desde el navegador. En el micro:bit se configura UART con  uart.init(115200) y finalmente se envia una lista de valores cada 100 ml, lo establecido, dando las
direcciones del micro:bit como la posicion en X y Y y los botones A y B.

Los valores mas especificos enviado al micro:bit son: 

xValue: valor del acelerómetro en el eje X 

yValue: valor del acelerómetro en el eje Y

aState: True o False si el boton A está presionado

bState: True o False si el boton B está presionado

## ¿Cómo es la estructura del protocolo ASCII usado?
La estructura ASCII es: 

X,Y,A,B\n

Donde se puede ver que estan separados por "," y fi8nalmente un /n que indica el final de cada paquete de datos

## Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.
La pregunta hacehaciendo refernecia aetsa parte del codigo: 
    
    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          microBitX = int(values[0]) + windowWidth / 2;
          microBitY = int(values[1]) + windowHeight / 2;

Donde se puede ver como se lee una línea completa terminada en \n, se eliminan espacios extra con .trim() para posteriormente dividirlo por  comas ",". Se transforman a int() y se ajustan al centro de la pantalla; para esto se suma windowWidth / 2 o windowHeight / 2 a las coordenadas
lo que convierte los valores del acelerometro en coordenadas que se pueden usar en el canvas.

## ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?
Esto se genera al en el codigo comprobar el estado anterior, el cual puede ser "False" o "True", cuando se ve un cambio del primero al segundo es cuando se determina si la accion del boton presionado se llevo acabo, en el codigo se puede ver como: 

    function updateButtonStates(newAState, newBState) {
      if (newAState === true && prevmicroBitAState === false) {
        // A PRESSED
        lineModuleSize = random(50, 160);
        clickPosX = microBitX;
        clickPosY = microBitY;
        print("A pressed");
      }
    
      if (newBState === false && prevmicroBitBState === true) {
        // B RELEASED
        c = color(random(255), random(255), random(255), random(80, 100));
        print("B released");
      }
    
      // Guardar los estados anteriores para detectar transiciones
      prevmicroBitAState = newAState;
      prevmicroBitBState = newBState;
    }


## Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

![image](https://github.com/user-attachments/assets/1b5cb939-35fd-47c5-ad33-6e0816daa6c3)

![image](https://github.com/user-attachments/assets/4e022eae-47db-4879-9d14-1b29687125ad)

