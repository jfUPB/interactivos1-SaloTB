# Controlando la Pantalla con una Máquina de Estados y Concurrencia
## Explicación donde muestres cómo este programa logra hacer varias cosas a las vez 
El programa tiene la capacidad de hacer varias acciones al mismo tiempo pues en lugar de ejecutar todas las tareas en orden, el programa cambia, "se mueve" entre sus estaods (STATE_HAPPY, STATE_SMILE, STATE_SAD), Esto a traves de la pulsacion de un boton 
o el tiempo que pasa y esta determinado por los estados inciales llamados intervalos; utime.ticks_ms() se usa para medir el tiempo sin detener el flujo del programa y asi que el mismo pueda reaccionar tanto al tiempo transcurrido como a la acciion
de los botones orpimidos. 

## Describe y aplica al menos 3 vectores de prueba para el programa.




