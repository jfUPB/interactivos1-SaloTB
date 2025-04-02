# Caso de estudio: p5.js

## Analicis primeros codigos
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


## Analicis codigo final
Determina si el micro bit esta conectado e incializa todo lo necesario para empezar a dibujar 

    if (microBitConnected === true) { //condicion del micro:bit 

    // Preparo todo para el estado en el próximo frame
    print("Microbit ready to draw");
    strokeWeight(0.75);
    c = color(181, 157, 0);
    noCursor();


