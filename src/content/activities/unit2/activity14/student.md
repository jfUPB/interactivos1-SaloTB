# Probando y Depurando la Bomba
## Vector de prueba 1 
Objetivo: se quiere probar que al orpimir el sensor superior la bomba se reestablesca correctamente 
Eventos generaods: Al orpimir el sensor superior la bomba deveria de volver al evento de configuracion y por ende reiniciar todo su proceso para volver a inciar el ciclo esperado
Prueba: el boton no estaba reaccionando correctamente a la llamada por culpa de un mal nombramiento del mismo, tras arregrarlo gracias alas refewrencioas el boton aun solo parecer funcionar cuandfo este mismo se deja precionado por un tiempo determinado
pero finalmente logra reiniciar el proceso de la bomba y actuar como es debido

## Vector prueba 2
Objetivo: Det6erminar si el maximo de cuenta en la bomba es 60s como deberia, y si este se puede modificar correctamente
Eventos generados: Al oprimir el boton "a" hasta llegar al numero 60 la cuenta se debe detener en la pantalla gracias a la funcion establecida "MAX_TIME = 60" y si esta es cambiada el minimo deberia cambiar en concecuencia
Prueba: al probar el programa se cumple lo establecido previamente y la cuenta regresiva es modificable con un nuevo limite de tiempo sin afectar el resto del funcionamiento de la bomba (MAX_TIME = 30) Sin emabrgo en este caso si se establece un numero
menor que el numero con el que se incia la cuenta regresiva de la bomba (en este caso 20) la bomba aun inciara en este numero incial, pero si lo reduces no te dejara volver al mismo gracias al limte establecido (MAX_TIME = 18) 

## Vector prueba 3
Objetivo: Determinar si el minimo de cuenta en la bomba es 10s como deberia, y si este se puede modificar correctamente
Eventos generados: Al oprimir el boton "b" hasta llegar al numero 10 la cuenta se debe detener en la pantalla gracias a la funcion establecida "MIN_TIME = 10" y si esta es cambiada el minimo deberia cambiar en concecuencia
Prueba: al probar el programa se cumple lo establecido previamente y la cuenta regresiva es modificable con un nuevo limite de tiempo sin afectar el resto del funcionamiento de la bomba (MIN_TIME = 5)  Sin emabrgo en este caso si se establece un numero
Mayor que el numero con el que se incia la cuenta regresiva de la bomba (en este caso 20) la bomba aun inciara en este numero incial, pero si lo aumentas no te dejara volver al mismo gracias al limte establecido (MIN_TIME = 21|) 

## Vector prueba 4


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
                display.show(str(remaining_time))  # Muestra el tiempo restante
            else:
                current_state = STATE_EXPLODED  # Cambia al estado de explosión
    
        elif current_state == STATE_EXPLODED:
            display.show(Image.SKULL)  # Muestra una calavera en el display
            speaker.on()
            audio.play(Sound.SOARING)  # Activa el speaker (buzzer)
    
            # Reiniciar la bomba al tocar el botón touch (simulado con pin1)
            if pin_logo.is_touched():
                current_state = STATE_CONFIG
                countdown_time = 20 # Restablece el tiempo inicial
                speaker.off()
