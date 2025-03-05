# Produciendo Sonidos con el Micro:bit
## Codigo

    from microbit import *
    import music
    
    uart.init(baudrate=115200)
    display.show(Image.BUTTERFLY)
    
    while True:
        if button_a.is_pressed():
            music.set_tempo(bpm=200)
            music.play(['c', 'c', 'f', 'f', 'g', 'g', 'f'])
            sleep(900)
            music.set_tempo(bpm=500)
            music.play(['f', 'e', 'g', 'a', 'c', 'g', 'e'])
            sleep(500)
        if button_b.is_pressed():
            music.set_tempo(bpm=30)
            music.play(music.POWER_UP)
## Documentación del código y descripción del proceso.
Utilizando los botones del micro:bit y la base de los sonidos en micro:bit python genere variaciones de sonidos con notas musicales y altere una cancion ya en el micro:bit alterando sus velocidades y tiempo de ejecucion. 
