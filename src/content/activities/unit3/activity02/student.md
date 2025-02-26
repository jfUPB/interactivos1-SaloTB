# Bomba 2.0
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
    
    # Secuencia para desactivar la bomba
    desarmar_secuencia = ["A", "B", "A", "SHAKE"]
    input_sequence = []
    
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
                input_sequence = []  # Reiniciar la secuencia de desactivación
    
        elif current_state == STATE_ARMED:
            elapsed_time = (utime.ticks_diff(utime.ticks_ms(), start_time) // 1000)
            remaining_time = countdown_time - elapsed_time
    
            if remaining_time > 0:
                display.show(str(remaining_time))
    
                # Captura de la secuencia de desactivación
                if button_a.was_pressed():
                    input_sequence.append("A")
                elif button_b.was_pressed():
                    input_sequence.append("B")
                elif accelerometer.was_gesture("shake"):
                    input_sequence.append("SHAKE")
    
                # Verificar si la secuencia es correcta
                if input_sequence == desarmar_secuencia:
                    display.show(Image.SILLY)
                    utime.sleep(1)
                    current_state = STATE_CONFIG  # Regresa al estado inicial
                    countdown_time = 20  # Reiniciar tiempo
                    input_sequence = []  # Limpiar secuencia
    
            else:
                current_state = STATE_EXPLODED  # Cambia al estado de explosión
    
        elif current_state == STATE_EXPLODED:
            display.show(Image.SKULL)  # Muestra una calavera en el display
            audio.play(Sound.SOARING)  # Activa el speaker (buzzer)
    
            # Reiniciar la bomba al tocar el botón touch (simulado con pin1)
            if pin1.read_digital():
                current_state = STATE_CONFIG
                countdown_time = 20  # Restablece el tiempo inicial
                audio.play(Sound.SOARING)

Implemente la secuencia de desactivacion como un array que contiene los pasos, luego un array vacio que servira para comprobar que los pasos sean utilizados en orden, a cada paso llamados "A", "B", "A", "Shake" se le asignan las acciones en el micro:bit, en este caso button.press_a, button.press_b, y "SHAKE", esta informacion se guarda en el array vacio y luego se iguala con el array de la secuencia y si ambos son iguales se ejecuta la opcion de desarmado, si no coinciden seguira hasta la explocion. Al entrar a la parte de desarmado se mostrara la imagen "SILLY" y luego volvera al estado de configuracion reiniciando el tiempo y el array vacio paraq ue todo pueda volver al ciclo incial. 
