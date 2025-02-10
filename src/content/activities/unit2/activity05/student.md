# Leyendo Datos Seriales
## Codigo P5.js
    let port;
    let connectBtn;
    
    function setup() {
        createCanvas(400, 400);
        background(220);
        port = createSerial();
  
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(100, 200);
    connectBtn.mousePressed(connectBtnClick);
  
    let sendBtn = createButton('Send h');
    sendBtn.position(240, 200);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
   
    }
    
    function draw() {



    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
    }
    
    function connectBtnClick() {
        if (!port.opened()) {
            port.open('MicroPython', 115200);
        } else {
            port.close();
        }
    }
    
    function sendBtnClick() {
        port.write('h');
    }
## Codigo micro:bit Python
    from microbit import *
    
    uart.init(baudrate=115200)
    display.show(Image.BUTTERFLY)
    
    while True:
        if uart.any():
            data = uart.read(1)
            if data:
                if data[0] == ord('h'):
                    display.show('h')
                    sleep(500)
                    display.show(Image.ANGRY)
## Documentación
Utilizando el codigo original de send love y eliminando codigo inesesario tanto en P5.js como en micro:bit Python realice el proceso de enviar desde el puerto serial, en este caso desde el computador al mirco:bit la misma infromacion, siendo en este 
caso la letra 'h'. Esta se envia al ejecutarse la funcion conectada al boton 'send h' y esto hace que se muestre en el micro:bit gracias al codigo de Python la misma letra. 
