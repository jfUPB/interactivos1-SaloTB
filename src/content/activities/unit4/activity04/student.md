## Caso de estudio: p5.js

### Analicis 
    function preload() {
      lineModule[1] = loadImage("02.svg");
      lineModule[2] = loadImage("03.svg");
      lineModule[3] = loadImage("04.svg");
      lineModule[4] = loadImage("05.svg");
    }
Carga imagenes desde el incio para guardarlas en un array. Estas imagenes siendo posible ser usadas como pinceles 

    const STATES = {
      WAIT_MICROBIT_CONNECTION: "WAIT_MICROBIT_CONNECTION",
      RUNNING: "RUNNING",
    };

Tiene dos estados posibles de la apliacion donde en una espera la coneccion del micro bit y en otra corre el programa de forma normal

    function setup() {
      createCanvas(windowWidth, windowHeight); // Crea un lienzo del tamaño de la ventana
      background(255); // Fondo blanco
    }
Se incialicia el canvas con todas sus caracteristicas

    function draw() {
      switch (appState) {
        case STATES.WAIT_MICROBIT_CONNECTION:
          break;
    
        case STATES.RUNNING:
          break;
      }
    }
Dependiendo del estado de la aplicacion determina su siguiente accion, o ejecuta la logica de dibujo o espera a la coneccion con el micro:bit 


    let port; // objeto que maneja la conexion serial del micro:bit 
    let connectBtn; // Boton para conectar y desconectar el micro:bit 
    let microBitConnected = false; // Determina si el micro:bit esta conectado (boolean)
Micro:bit 

    function setup() {
      createCanvas(windowWidth, windowHeight);
      background(255);
      port = createSerial(); // Inicializa el objeto serial
      connectBtn = createButton("Connect to micro:bit"); // Crea un botón
      connectBtn.position(0, 0);
      connectBtn.mousePressed(connectBtnClick); // Asigna evento de clic
    }
Inicializa las caracteristicas del canvas y tambien crea el boton para conecatr el micro:bit y determina el evento de oprimir este mismo boton

    function connectBtnClick() {
      if (!port.opened()) {
        port.open("MicroPython", 115200);
      } else {
        port.close();
      }
    }
Logica de coneccion con el micro:bit 


Determina si el micro bit esta conectado e incializa todo lo necesario para empezar a dibujar 

    if (microBitConnected === true) { //condicion del micro:bit 

    // Preparo todo para el estado en el próximo frame
    print("Microbit ready to draw");
    strokeWeight(0.75);
    c = color(181, 157, 0);
    noCursor();
Se declaran las variables globales tales como el color actual, el tamaño de la linea, la rotacion entre oitras

    let c;
    let lineModuleSize = 0;
    let angle = 0;
    let angleSpeed = 1;
    const lineModule = [];
    let lineModuleIndex = 0;
    let clickPosX = 0;
    let clickPosY = 0;

Se declaran las variables del micro:bit como movimeinto y posicion ademas de su estado antes y despues de oprimir los botones A y B

    let microBitX = 0;
    let microBitY = 0;
    let microBitAState = false;
    let microBitBState = false;
    let prevmicroBitAState = false;
    let prevmicroBitBState = false;

Detecta los eventos al presionar A y B ya sea para cambair el color o el pincel

    function updateButtonStates(newAState, newBState) {
      if (newAState === true && prevmicroBitAState === false) { 
        lineModuleSize = random(50, 160); 
        clickPosX = microBitX;
        clickPosY = microBitY;
        print("A pressed");
      }
      if (newBState === false && prevmicroBitBState === true) {
        c = color(random(255), random(255), random(255), random(80, 100));
        print("B released");
      }
    
      prevmicroBitAState = newAState;
      prevmicroBitBState = newBState;
    }
Lectura del puerto serial y si el mismo esta abierto espera 4 valores: A, B, X, Y

    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      ...
    }
En esta prate se gestionan los estados, esperando a que el micro:bit se conecte o dibujando dependienod del estado del boton A

    switch (appState) {
      case STATES.WAIT_MICROBIT_CONNECTION:
        ...
      case STATES.RUNNING:
        ...
    }


### Preguntas

#### ¿Para qué se usan estas imágenes? ¿Qué representan?
Las i9magenes utilizadas en el codigo se utilizan para poder cambiar los tipos de pincel, cada una de estas podria decrise es uno de los pinceles que podemos utilizar para dibujar en el canvas

####  ¿Qué pasaría si el puerto está cerrado y el micro:bit envía datos?
Si esta cerrado el micro:bit seguiria transmitiendo ya sea usando print() o serial.write() en MicroPython pero el navegador (p5.js) simplemente no los recibe y no habria errores ni excepciones en el sketch de p5.js. Anque al final el draw() nunca cambiaria al estado RUNNING.

#### Data = "{},{},{},{}\n".format(xValue, yValue, aState, bState) ¿Qué pasaría si el micro:bit no envía el "\n"?
La /n lo que le dice al programa es que lea datos del puerto serial hasta que haya un salto de linea, por lo que si esto nunca llega entonces los valores del micro:bity y el micro:bitx no se actualizan, la interfaz se congelaria y updateButtonStates() no se llamraia. 

#### ¿Por qué se suma windowWidth/2 y windowHeight/2 a los valores de x e y?
Para trasladar el sistema de coordenadas del micro:bit al centro del canvas de p5.js, pues las cordenadas predeterminadas del micro:bit son [0,0] lo que en p5.js es la esquina superior izquierda del canvas. 

#### ¿Cómo puedes verificar que los eventos de keypressed y keyreleased se están generando?
Esto se podria verificar de varias maneras como escribir la accion realizada por el evento en la consola o determinar una reaccion en el micro:bit una accion en especifico que se lleve a cabo cada vez que se realice la accion (Esto puede ser un sonido o una pista visual) 

####  Algoritmo updateButtonStates. ¿Qué hace? ¿Por qué es necesario almacenar el estado anterior de los botones? ¿Qué pasaría si no se almacenara el estado anterior?
Es una funcion que maneja las transiciones de estado, por esto es neceario detectar el estado anterior, para asi saber cuando se esta generando un cambio. No podria detectar cuando se deja presionar "B" y el boton "A" se ejecutaria de forma infinita.

#### ¿Qué pasó con algunos eventos del mouse? 
Los eventos del mause inicalmente usados en el codigo original son remplazados por acciones en el micro:bit. Sin emabrgo se podrian usar tanto los eventos del mause como los eventos del micro:bit 

### No se están recibiendo 4 datos del micro:bit ¿Qué significa esto? ¿Qué puedes hacer para solucionar este problema?
Este mensaje popdria estar relacionado a la parte del codigo que qu hace la lectura del puerto serial que espera resibir 4 daqtos: A,B,x,Y. Puyede que este porblema se este causando porque espera los datos de forma simultanea y estos no estan llegando como es debido. 
