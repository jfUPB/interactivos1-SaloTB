# Bomba 3.0
    from microbit import *
    import utime
    
    # Definición de estados
    STATE_CONFIG = 0
    STATE_ARMED = 1
    STATE_EXPLODED = 2
    
    # Configuración inicial
    current_state = STATE_CONFIG
    countdown_time = 20  # Tiempo inicial de la bomba (20 segundos)
    start_time = 0
    
    # Límites de tiempo
    MIN_TIME = 10
    MAX_TIME = 60
    
    # Definicion de Eventos
    isEvent= False
    DataEvent= ""
    
    # Secuencia para desactivar la bomba
    desarmar_secuencia = ["A", "B", "A", "SHAKE"]
    input_sequence = []
    
    def tareaBomba():
        global isEvent
        global Data
        global countdown_time
        global current_state
        global start_time
        global input_sequence
        
        current_state = STATE_CONFIG
        display.show(str(countdown_time))
        if isEvent == True:
            
            if DataEvent == "A":
               countdown_time += 1
               isEvent = False
            elif DataEvent == "B":
               current_state = STATE_CONFIG
               countdown_time -= 1
               isEvent = False
            elif DataEvent == "S":
               accelerometer.was_gesture("shake")
               current_state = STATE_ARMED
               start_time = utime.ticks_ms()
               input_sequence = []  # Reiniciar la secuencia de desactivación
               isEvent = False
        if current_state == STATE_ARMED:
            elapsed_time = (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000)
            remaining_time = countdown_time - elapsed_time
    
            if remaining_time > 0:
                display.show(str(remaining_time))
    
             # Captura de la secuencia de desactivación
            elif isEvent == True:
                isEvent = False
                if DataEvent == "A":
                  input_sequence.append("A")
                if DataEvent == "B":
                  input_sequence.append("B")
                if DataEvent == "S":
                   input_sequence.append("SHAKE")         
                    
                # Verificar si la secuencia es correcta       
            if input_sequence == desarmar_secuencia:
                display.show(Image.SILLY)
                utime.sleep(1)
                current_state = STATE_CONFIG  # Regresa al estado inicial
                countdown_time = 20  # Reiniciar tiempo
                input_sequence = []  # Limpia secuencia
    
            else:
                current_state = STATE_EXPLODED  # Cambia al estado de explosión
    
        elif current_state == STATE_EXPLODED:
            display.show(Image.SKULL)  # Muestra una calavera en el display
            audio.play(Sound.SOARING)  # Activa sonido
    
            # Reiniciar la bomba al tocar el botón touch (simulado con pin1)
            if pin1.read_digital():
                current_state = STATE_CONFIG
                countdown_time = 20  # Restablece el tiempo inicial
                audio.play(Sound.SOARING)
                
    def tareaEventos():
        if button_a.was_pressed():
            isEvent == True
            DataEvent == "A"
        if uart.any():
            data = uart.read(1)
            if data:
                if data[0] == ord('A'):
                  isEvent == True
                  DataEvent == "A"
        
    while True:
       tareaBomba()
       tareaEventos()
