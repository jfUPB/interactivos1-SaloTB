# Caso de estudio: micro:bit

    # Imports go at the top
    from microbit import *
    
    uart.init(115200) // permite enviar datos del micro:bit a otro dispositivo
    display.set_pixel(0,0,9) //Enciende un led para mostrar que esta funcionando
    
    while True:
        xValue = accelerometer.get_x()
        yValue = accelerometer.get_y()
        aState = button_a.is_pressed()
        bState = button_b.is_pressed()
        data = "{},{},{},{}\n".format(xValue, yValue, aState,bState)
        uart.write(data)
        sleep(100) # Envia datos a 10 Hz

Se estan enviando cuatro lineas de infromacion el valor de y, el valor de x (Posicion del micro:bit) y el estado de los botones A y B, lo que isgnifica que determina si el boton esta precionado "True" o si no esta precionado "False". 

Si los datos no estuviesen separados por comas dejarian de ser un conjunto de datos y serian un dato individual, y sin el salto de la linea se mostraria una unica linea pues se sobreescribiria sobvre si mismo los datos resividos en el tiempo.

La funcion sleep se utiliza para darle un tiempo al codigo antes de enviar el siguiente conjunto de datos, si no se utilizara se enviarian constantemente sin pausa alguna, seria demasidos en un solo segundo y no se podria leer ni revisar correctamente.

Caundo se inclina hacia abajo: "x" es negativo alrededor de -240 y "y" es positivo alrededor de 100
Caundo se inclina hacia arriba: "X" se mantiene negativo alrededor de -200 y "y" es negativo alre4dedor de -800
Cuando se inclina hacia la derecha: "x" es popsitivo alrededor de 900 y "y" se vuelve negativo alrededor de -40
Cuando se inclina hacia la izquierda: "x" es negativo alrededor de -1000 y "y" es positivo alrededor de 40

Caundo se utiliza "was" en vez de "is" a la hora de presionar los botones el cambio se eviendcia en que al usar "is" se puede mantener el boton preisonado lo que genera que el resultado actual y los posteriores sean "True", en cmabio utilizando "Was" solo dara un cambio y este sera moestrado cuando se deje de oprimir el boton. 
