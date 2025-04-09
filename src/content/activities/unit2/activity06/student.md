# Generando Salidas Visuales
    # Imports go at the top
    from microbit import *
    import music
    
    
    # Code in a 'while True:' loop repeats forever
    while True:
        if button_a.was_pressed():
            display.show('A') 
        if button_b.was_pressed():
             display.show(Image.SILLY)
        if accelerometer.was_gesture('shake'):
            display.show(Image.CLOCK12)
            
El codigo muestra al oprimir el boton a la letra "A", al presionar el boton b, la imagen silly, y al moverlo la imagen CLOCK12, todo utilizando display y no scroll, por lo que la simagenes permaneces estaticas en el micro:bit 
y permanecesn en pantalla hasta que otra sea mostrada
