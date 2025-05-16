# Controla la bomba desde tu sketch en p5.js
## P5.js

    let port;
    let connectBtn;
    
      function setup() {
    
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(150, 150);
    connectBtn.mousePressed(connectBtnClick);
    
    let sendBtn = createButton('Send A');
    sendBtn.position(120, 200);
    sendBtn.mousePressed(sendBtnClick);
    
    let Bot2 = createButton('Send B');
    Bot2.position(120, 220);
    Bot2.mousePressed(sendBtnClick2);
      
    let Bot3 = createButton('Send S');
    Bot3.position(220, 220);
    Bot3.mousePressed(sendBtnClick3);
      
    let Bot4 = createButton('Send T');
    Bot4.position(220, 200);
    Bot4.mousePressed(sendBtnClick4);
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
        port.write('A');
    }
    
    function sendBtnClick2() {
        port.write('B');
    }
    
    function sendBtnClick3() {
        port.write('S');
    }
    
    function sendBtnClick4() {
        port.write('T');
    }

  ## Micro:bit 
    from microbit import *
    import utime
    
    # Definicion de estados
    STATE_CONFIG = 0
    STATE_ARMED = 1
    STATE_EXPLODED = 2
    
    # Configuracion inicial
    current_state = STATE_CONFIG
    countdown_time = 20  
    start_time = 0
    
    # Limites de tiempo
    MIN_TIME = 10
    MAX_TIME = 60
    
    # Definicion de eventos
    isEvent = False
    DataEvent = ""
    
    # Secuencia para desactivar la bomba
    desarmar_secuencia = ["A", "B", "A", "S"]
    input_sequence = []
    
    def tareaBomba():
        global isEvent, DataEvent, countdown_time, current_state, start_time, input_sequence
    
        if current_state == STATE_CONFIG:
            display.show(str(countdown_time))  # Muestra el tiempo en pantalla
            
            if isEvent:  # Solo procesa eventos cuando ocurren
                if DataEvent == "A" and countdown_time < MAX_TIME:
                    countdown_time += 1
                elif DataEvent == "B" and countdown_time > MIN_TIME:
                    countdown_time -= 1
                elif DataEvent == "S":
                    current_state = STATE_ARMED
                    start_time = utime.ticks_ms()
                    input_sequence = []  # Reiniciar secuencia de desactivacion
                
                isEvent = False  # fin del evento
            
        elif current_state == STATE_ARMED:
            elapsed_time = utime.ticks_diff(utime.ticks_ms(), start_time) // 1000
            remaining_time = countdown_time - elapsed_time
    
            if remaining_time > 0:
                display.show(str(remaining_time))
                
                if isEvent:  # Capturar la secuencia de desactivacion
                    if DataEvent in ["A", "B", "S"]:
                        input_sequence.append(DataEvent)
    
                    # Verificar si la secuencia es correcta
                    if input_sequence == desarmar_secuencia:
                        display.show(Image.HAPPY)
                        utime.sleep(1)
                        current_state = STATE_CONFIG  # Reiniciar bomba
                        countdown_time = 20
                        input_sequence = []
    
                    isEvent = False  
    
            else:
                current_state = STATE_EXPLODED  
    
        elif current_state == STATE_EXPLODED:
            display.show(Image.SKULL)  
            audio.play(Sound.SOARING)  
    
            if isEvent and DataEvent == "T":  # Reiniciar bomba con boton touch (T)
                current_state = STATE_CONFIG
                countdown_time = 20
                audio.play(Sound.SOARING)
                isEvent = False  # fin del evento
    
    def tareaEventos():
        global isEvent, DataEvent
    
        if button_a.was_pressed():
            isEvent = True
            DataEvent = "A"
        elif button_b.was_pressed():
            isEvent = True
            DataEvent = "B"
        elif accelerometer.was_gesture("shake"):
            isEvent = True
            DataEvent = "S"
        elif pin1.read_digital():
            isEvent = True
            DataEvent = "T"
    
        # Leer eventos del puerto serial p5.js
        if uart.any():
            data = uart.read(1)
            if data:
                if data[0] == ord('A'):
                    isEvent = True
                    DataEvent = "A"
                if data[0] == ord('B'):
                    isEvent = True
                    DataEvent = "B"
                if data[0] == ord('S'):
                    isEvent = True
                    DataEvent = "S"
                if data[0] == ord('T'):
                    isEvent = True
                    DataEvent = "T"
                    
    
    # Configurar UART para comunicación serial
    uart.init(baudrate=115200)
    
    while True:
        tareaEventos()
        tareaBomba()

    
    
    
