#### Interacción básica con micro:bit

##### Micro:bit

    from microbit import *
    
    uart.init(baudrate=115200)
    display.show(Image.BUTTERFLY)
    
    while True:
        if button_a.is_pressed():
            uart.write('A')
            sleep(500)

##### p5.js

    let port;
    let connectBtn;
    
    function setup() {
        createCanvas(400, 400);
        background(220);
        port = createSerial();
        connectBtn = createButton('Connect to micro:bit');
        connectBtn.position(135, 300);
        connectBtn.mousePressed(connectBtnClick);
        fill('white');
        square(150, 150, 100)
    }
    
    function draw() {
    
      if(port.availableBytes() > 0){
            let dataRx = port.read(1);
            if(dataRx == 'A'){
                fill('#673AB7');
            }
       
        background(220);
        square(150, 150, 100)
        fill('black');
        text(dataRx, width / 2, height / 2);
      }
    
    
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

##### Proceso de conexion 

1. Se conecta el micro:bit en el puerto usb de la computadora
2. En micro:bit Python Editor se ingreso el codigo proporcionado por el profesor y tras un analisis de las partes necesarias para la actividad se retira todo aquello que se considera inecesario
En este caso unicamente dejando la accion del boton y finalment6e cargando el codigo al micro:bit
3. Se realiza el codigo en p5.js utilizando el codigo proporcionado por el profesor como base, se eliminan lienas inesesarias como el boton de "send love" y se cambia la elipse con el cuadrado de las
referencias, finalmente se elije un color y se ajusta la ubicacion de los objetos.
4. Se comprobo que todo funcionace correindolo con el microbit.

##### Comunicacion entre dispositivos

La comunicacion entre los dispositivos es similar a las ya trabajadas, en este caso el microbit actua como dispositivo de entrada al tenmer el boton y el computador es el dispositivo de salida al mostrar
el color especificado.


  
