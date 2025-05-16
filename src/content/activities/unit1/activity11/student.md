#### Control de movimiento con micro:bit

##### Micro:bit 

    from microbit import *
    
    uart.init(baudrate=115200)
    display.show(Image.BUTTERFLY)
    
    while True:
        if button_a.is_pressed():
            uart.write('A')
            sleep(500)
        if button_b.is_pressed():
            uart.write('B')
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
        circle(200, 200, 100)
    }
    
    function draw() {
      
       y = random(0,400)
       x = random(0,400)
    
    
       if(port.availableBytes() > 0){
            let dataRx = port.read(1);
     
        background(220);

        if(dataRx == 'A'){
          circle(x, 0, 100)
            
        }
        else if(dataRx == 'B'){
            circle(200, y, 100)
        }
     
       // circle(x, y, 100)
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

##### Mapeo de los botones
El movimiento de A y B esta determinado por la funcion random() donde se determina que pueden moverse de forma aleatoriaq cada vez que se opime el boton, sinmeabrgo A esta limitado en "y" y solo se mueve en x
y B esta limitado en "x" por lo que solo se mueve en y. Esto ocurre ya que solo se ponen las variables afectadas por random() en esos respectivas posiciones y la sobrante se establece como 0. 
Asi el movimiento es aleatorio pro todas la pantalla, pero se puede predecir si se movera de forma horizontal o vertical dependiendo del boton elegido. 
