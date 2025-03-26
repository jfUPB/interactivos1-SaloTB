# Manipulando Entradas Digitales
## 1 ¿Qué querías comprobar?
Quiero comprobar que al poner una funcion en el boton b que se active al ser presionado de forma constante me dara una reaccion, mientars que si se pone otra de forma instantanea me dara otra, esta es para comprobar que tan 
exacto es el boton al determinar si la presion ejercida es constante o momentanea. (is or was)
## 1 ¿Cuál fue tu hipótesis?
Al presionar el botopn b y tener ambas funciones funcionando a la par se reproduciran al mismo momento pues reconocera el mantenerlo presionado y el presionarlo y dejaqrlo de presionar al mismo tiempo, pero si se mantiene el
boton presionado la funcion de "is" continuara funcionando porlo que la imagen se sguira mostrando mientars que la funcion "was" dejara de mostrarse en el microbit 
## 1 Los códigos involucrados en el experimento
    # Imports go at the top
    from microbit import *
    
    
    # Code in a 'while True:' loop repeats forever
    while True:
        if button_b.was_pressed():
            display.scroll('A') 
        if button_b.is_pressed():
            display.scroll('B') 
## 1 Descripción de lo resultados
Al oprimir el boton de forma inmediata solo se lee la "A" una unica vez, que corresponde a la funcion "Was"
Mientras que si se deja presionado el boton por un rato se lee la "B" consecutivamente de la "A" una uniuca vez 
## 1 Análisis de esos resultados
Se puede inferir que el microbit no detecta el "is" cuando el boton no se deja oprimido por mas de cierto tiempo, al igual que se puede inferir que al ser presionado por el tiempo necesario el microbit le dara prioridad o
reproducira primero la funcion "is" a causa de que "Was" se tiene en cuenta cuando se suelta el boton o ya pasa el tiempo estimado que se considera como el que se oprime el boton. Sin emcnionar que no importa cuanto
tiempo extra este se deje presioando este no inciara el proceso de mostrar las letras otra vez ni continuara mostrando a "B". 
## 1 Conclusiones
La geraquia en el codigo no es relevante con respecto a cuando o que imagen se muestra primero, sino la interpretacion de la precion del boton por parte del micro:bit siendo en este caso que se necesita cierto tiempo para
que se considere una precion constante y que si ese es el caso esta se reproducira primero que el "was"

## 2 ¿Qué querías comprobar?
¿Que sucede cuando dos botones con diferentes ouputs son precionados al mismo tiempo?

## 2 ¿Cuál fue tu hipótesis?
Piensoq ue el micro:bit determinara al azar o dependiendo del error humano al preisonarlos al mismo tiempo para darles un orden en su aparicion en el output, tambien podria decidir el orden de aparicion popr orden de codigo

## 2 Los códigos involucrados en el experimento
Primera prueba:

    # Imports go at the top
    from microbit import *
    
    
    # Code in a 'while True:' loop repeats forever
    while True:
        if button_a.was_pressed():
            display.scroll('A') 
        if button_b.was_pressed():
            display.scroll('B') 
Segunda prueba: 

    # Imports go at the top
    from microbit import *
    
    
    # Code in a 'while True:' loop repeats forever
    while True:
        if button_a.was_pressed():
            display.show('A') 
        if button_b.was_pressed():
            display.show('B') 
            
## 2 Descripción de lo resultados
AL usar el primer codigo que utiliza "scroll" osea que las letras entran y salen del output ambas letras se turnan en aparecer de forma aleatorea, sin emabrgo note que el orden "B" "A" era mas comun. e

Al utilizar el segundo codigo las letras no desaparecen de la pantalla por lo que se "pelean" por aparecer en pantalla, esta vez dependienod de que boton fue oprimido primero, en ocaciones superponiendose el uno sobre el otro

## 2 Análisis de esos resultados
La razon de la aparicion de "B" y "A" en ese orden puede deberse a mi propia velocidad al oprimir los botones, por lo que la base para decidir la apricion no tiene nada que ver ocn el codigo y esta directamente relacionada
a la velocidad del usuario. 

## 2 Conclusiones
Los resultados demuestran que las letras dependiendo del espacio que ocuipen en al pantalla púeden actuar de forma distinta y la gerarquia de aparicion en los led es dependiente de la velocidad con la que el usuario oprima 
los botones
