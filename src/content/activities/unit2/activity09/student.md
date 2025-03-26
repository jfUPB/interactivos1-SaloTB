# Implementando un Semáforo con Máquina de Estados 
    
    crobit import *
    import utime
        
    class Semaforo:
        def __init__(self, x, y):
                self.x = x
                self.y = y
                self.state = "Rojo"  # Comienza en rojo
                self.startTime = utime.ticks_ms()
            
        def update(self):
            now = utime.ticks_ms()
            
            if self.state == "Rojo":
                display.clear()
                display.set_pixel(self.x, self.y, 9)  # Rojo encendido
                if utime.ticks_diff(now, self.startTime) > 3000:  # 3 segundos en rojo
                    self.startTime = now
                    self.state = "Amarillo"
            
            
            elif self.state == "Amarillo":
                display.clear()
                display.set_pixel(self.x, self.y + 1, 9)  # Amarillo encendido
                if utime.ticks_diff(now, self.startTime) > 5000:  # 2 segundos en amarillo
                    self.startTime = now
                    self.state = "Verde"
    
            elif self.state == "Verde":
                display.clear()
                display.set_pixel(self.x, self.y + 2, 9)  # Verde encendido
                if utime.ticks_diff(now, self.startTime) > 4000:  # 5 segundos en verde
                    self.startTime = now
                    self.state = "Rojo"
     
    semaforo = Semaforo(2, 0)
    
    while True:
        semaforo.update()
    

