# Implementando la Bomba Temporizada

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
    
    while True:
        if current_state == STATE_CONFIG:
            display.show(str(countdown_time))  # Muestra el tiempo en pantalla
    
            # Ajuste del tiempo con los botones
            if button_a.was_pressed() and countdown_time < MAX_TIME:
                countdown_time += 1
            elif button_b.was_pressed() and countdown_time > MIN_TIME:
                countdown_time -= 1
    
            # Activar la bomba con shake
            if accelerometer.was_gesture("shake"):
                current_state = STATE_ARMED
                start_time = utime.ticks_ms()
        
        elif current_state == STATE_ARMED:
            elapsed_time = (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000)
            remaining_time = countdown_time - elapsed_time
            
            if remaining_time > 0:
                display.scroll(str(remaining_time))  # Muestra el tiempo restante
            else:
                current_state = STATE_EXPLODED  # Cambia al estado de explosión
    
        elif current_state == STATE_EXPLODED:
            display.show(Image.SKULL)  # Muestra una calavera en el display
            pin0.write_digital(1)  # Activa el speaker (buzzer)
            
            # Reiniciar la bomba al tocar el botón touch (simulado con pin1)
            if pin1.read_digital():
                current_state = STATE_CONFIG
                countdown_time = 20  # Restablece el tiempo inicial
                pin0.write_digital(0)  # Apaga el speaker
