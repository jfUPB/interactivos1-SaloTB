# Actividad de los 3 semáforos

    from microbit import *
    import utime
    
    class Semaforo:
        def __init__(self, x, y, tiempo_rojo, tiempo_amarillo, tiempo_verde):
            self.x = x
            self.y = y
            self.state = "Rojo"  
            
            self.startTime = utime.ticks_ms()
            self.tiempo_rojo = tiempo_rojo
            self.tiempo_amarillo = tiempo_amarillo
            self.tiempo_verde = tiempo_verde
    
        def update(self):
            now = utime.ticks_ms()
    
            if self.state == "Rojo":
                display.set_pixel(self.x, self.y, 9)  
                if utime.ticks_diff(now, self.startTime) > self.tiempo_rojo * 1000:
                    self.startTime = now
                    self.state = "Amarillo"
                    display.clear()
    
            elif self.state == "Amarillo":
                display.set_pixel(self.x, self.y + 1, 6)  
                if utime.ticks_diff(now, self.startTime) > self.tiempo_amarillo * 1000:
                    self.startTime = now
                    self.state = "Verde"
                    display.clear()
    
            elif self.state == "Verde":
                display.set_pixel(self.x, self.y +2 , 4)  
                if utime.ticks_diff(now, self.startTime) > self.tiempo_verde * 1000:
                    self.startTime = now
                    self.state = "Rojo"
                    display.clear()
    
    semaforo1 = Semaforo(1, 0, 5, 2, 3)
    semaforo2 = Semaforo(2, 0, 3, 1, 2)
    semaforo3 = Semaforo(3, 0, 4, 3, 2)
    
    while True:
        semaforo1.update()
        semaforo2.update()
        semaforo3.update()

La ventaja en este caso de utilizar la "class semaforo" es que no se tienen que crear los mismos estados "rojo" "amarillo" y "verde" para cada uno de los semaforos, sino que se pueden reutilizar los originalmente nombrados con diferencias de tiempo y
ubicacion al llamrlos como objetos de la clase, asi cada objeto se basa en la clase utilizada y pasa por cada uno de los estados con sus propios poarametros que los hacen actuar de forma individual.
