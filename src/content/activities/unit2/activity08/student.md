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

      elif self.state == "WaitTimeout":
          if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
              self.startTime = utime.ticks_ms()
              if self.pixelState == 9:
                  self.pixelState = 0
              else:
                  self.pixelState = 9
              display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

    pixel1 = Pixel(0,0,0,1000)
    pixel2 = Pixel(4,4,0,500)
// 
    
    while True:
        pixel1.update()
        pixel2.update()
// Es un ciclo infinito, en el que se busca la direccion del pixel
## Estados

## Eventos

## Acciones


