#### Generando de imágenes en micro:bit

##### Micro:bit 

     uart.init(baudrate=115200)
     display.show(Image.BUTTERFLY)
    
     while True:
        if uart.any():
            data = uart.read(1)
            if data:
                if data[0] == ord('h'):
                    display.show(Image.HEART)
                    sleep(500)
                    display.show(Image.HAPPY)
                if data[0] == ord('b'):                
                    display.show(Image.SAD)
                    sleep(700)
                    display.show(Image.SKULL)
                if data[0] == ord('a'):
                    display.show(Image.SILLY)

##### p5.js
    let port;
    let connectBtn;

      function setup() {
  
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  
    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
  
    let Bot2 = createButton('Send HATE');
    Bot2.position(220, 320);
    Bot2.mousePressed(sendBtnClick2);
  
    let Bot3 = createButton('Send ???');
    Bot3.position(220, 340);
    Bot3.mousePressed(sendBtnClick3);
  
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
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
    
    
    
    function sendBtnClick2() {
        port.write('b');
    }
    
    
    function sendBtnClick3() {
    port.write('a');
}

##### Solución del problema
