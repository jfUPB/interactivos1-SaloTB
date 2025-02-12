# Analizando un Programa con Máquinas de Estados
## Programa y analicis detallado
    from microbit import *
    import utime
// Importa todas las funciones y clases necesarias para interactuar con la micro:bit 

    class Pixel:
        def __init__(self,pixelX,pixelY,initState,interval):
            self.state = "Init"
            self.startTime = 0
            self.interval = interval
            self.pixelX = pixelX
            self.pixelY = pixelY
            self.pixelState = initState
// Se incializa una clase que define un pixel individual en la matriz led, donde pixelx y pixely representan la direccion del pixel inistate el estado incial del pixel, e interval que simboliza el tiempo en milisegundos de cambio de estado del pixel

    def update(self):

      if self.state == "Init":
          self.startTime = utime.ticks_ms()
          self.state = "WaitTimeout"
          display.set_pixel(self.pixelX,self.pixelY,self.pixelState)
// Se lee el valor de Init que se incializo anteriormente y si se cumple la condicion este sigue adelante con la funcion startime que guarda la cantidad de tiempo que lleva el programa, y luego lo guarda en WaiTimeout para que asi se cumpla la condicion siguiente

      elif self.state == "WaitTimeout":
          if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
              self.startTime = utime.ticks_ms()
              if self.pixelState == 9:
                  self.pixelState = 0
              else:
                  self.pixelState = 9
              display.set_pixel(self.pixelX,self.pixelY,self.pixelState)
// Si se cumple que la cantidad de tiempo transcurrido es mayor que el intervalo de tiempo determinado como parametro, se cambia el estado del Led de encendido a apagado o viseversa

    pixel1 = Pixel(0,0,0,1000)
    pixel2 = Pixel(4,4,0,500)
// Se crean los objetos con los parametros establecidos incialmente en la clase, pero ahora se les dan valores, los dos primeros siendo la posiciones, el siguiente determina su incio 
    
    while True:
        pixel1.update()
        pixel2.update()
// Es un ciclo infinito, en el que se busca la direccion del pixel donde estan guardados los parametros anetriormente

## Estados
Los estados en el programa son Init y Waitimeout quienes representan el recorrido del tiempo del programa para confirmar que el parametro se cumpla y se ejecute correctamente 

## Eventos 
En el codigo existen varios eventos, en la mayoria se lee el tiempo transcurrido del programa, enotras palabras el evento depende de los estados y sus cambios, estos eventos se repiten hasta que la condiciones de los estados se cumpla y genere el cambio que lleva a la accion. Entre esos eventos esta el que confirma si la cantidad del tiempo transcurrido es igual o mayor al estipulado en el estado y otyro es el evento que hacve que el codigo se repita constantemente. 

## Acciones 
Las acciones del programa son el cambio del parametro inistate que representa el estado del boton, este siendo casmbiado en dos estado diferentes, encendido y apagado


