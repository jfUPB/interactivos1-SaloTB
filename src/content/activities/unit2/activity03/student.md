#### Explorando el Micro:bit y Micropython

##### Entradas y salidas Micro:bit 
1. El micro:bit tiene dos botones en la parte delantera que se pueden usar por separado o juntos para hacer que las cosas sucedan.
2. El nuevo micro:bit tiene una entrada extra. El logotipo dorado también funciona como sensor táctil. Puedes usarlo como un botón extra en tus programas, además de los botones A y B.
3. 25 LED dispuestos en una cuadrícula de 5x5 que pueden actuar como sensores, midiendo la cantidad de luz que cae sobre tu micro:bit.
4.Puedes crear programas que reaccionen a sonidos fuertes y silenciosos y medir los niveles de ruido con el micrófono integrado del nuevo micro:bit

1. 25 LED dispuestos en una cuadrícula de 5x5 componen la pantalla para mostrar imágenes, palabras y números.
2.  El LED del micrófono le muestra cuando el micrófono está midiendo activamente los niveles de sonido.
3.  El nuevo micro:bit con sonido tiene un altavoz incorporado para que puedas añadir música y nuevos sonidos a tus proyectos con mayor facilidad.
4.  El único LED en la parte posterior del micro:bit original parpadea cuando estás descargando un programa en él, y se enciende para mostrar que se está alimentando desde la toma USB.


##### Funciones Micropython

1.    if button_a.is_pressed():
            uart.write('A')
2.    if accelerometer.was_gesture('shake'):
        uart.write('C')
3.    if button_b.is_pressed():
        uart.write('B')

1.    display.show(Image.HEART)
2.    display.scroll('Hello')
3.    def greeting():
    display.scroll('Hello ' + name)

name = 'Sam'
greeting()
