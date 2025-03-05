# Bomba 3.0
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
    
        # Leer eventos del puerto serial
        if uart.any():
            data = uart.read(1)
            if data:
                char = data.decode('utf-8').strip()  
                if char in ["A", "B", "S", "T"]:  # Validar el evento
                    isEvent = True
                    DataEvent = char
    
    # Configurar UART para comunicación serial
    uart.init(baudrate=115200) # establece la velocidad de transmisión de datos en 115200 baudios (bits por segundo)
    
    while True:
        tareaEventos()
        tareaBomba()

## Explicacion
En este codigo se buscaba que la bomba funcionace desde el puerto cerial y el micro:bit por igual, y para lograr este funcionamiento realice dos funciones como fue sugerido por el profesor, TareaBomba y TareaEventos. En TareaEvento se resiven los datos tanto del puerto serial como del micro:bit, su funcionamiento se puede resumir en que cada vez que ocurre un evento "isEvent" se convierte en "True" y guarda el evento correspondiente en "DataEvent". En TareaBomba se controla bomba teniendo en cuenta los anteriores eventos (los ya utilizados en el anterior codigo de la bomba) "Configuracion", "Activada", "Explocion", leyendo las entradas del puerto serial y del micro:bit por igual. 
