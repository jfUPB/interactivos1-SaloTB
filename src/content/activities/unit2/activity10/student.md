# Controlando la Pantalla con una Máquina de Estados y Concurrencia
## Explicación donde muestres cómo este programa logra hacer varias cosas a las vez 
El programa tiene la capacidad de hacer varias acciones al mismo tiempo pues en lugar de ejecutar todas las tareas en orden, el programa cambia, "se mueve" entre sus estaods (STATE_HAPPY, STATE_SMILE, STATE_SAD), Esto a traves de la pulsacion de un boton 
o el tiempo que pasa y esta determinado por los estados inciales llamados intervalos; utime.ticks_ms() se usa para medir el tiempo sin detener el flujo del programa y asi que el mismo pueda reaccionar tanto al tiempo transcurrido como a la acciion
de los botones orpimidos. 

## Describe y aplica al menos 3 vectores de prueba para el programa.

###Vector de Prueba 1: Transicion automatica de STATE_HAPPY a STATE_SMILE
Condiciones Iniciales:
El sistema inicia en STATE_HAPPY
No se presiona ningun botón
Eventos generados:
Se deja pasar el tiempo sin intervención del usuario
Después de HAPPY_INTERVAL = 1500 ms, el sistema debería cambiar a STATE_SMILE
Resultados Esperados:
El sistema muestra la imagen Image.SMILE
El estado cambia a STATE_SMILE
Se reinicia el temporizador con SMILE_INTERVAL = 1000 ms
Resultados obtenidos:
Después de 1.5 segundos cambia a STATE_SMILE, el vector de prueba funciona

###Vector de Prueba 2: Botón A en STATE_HAPPY cambia a STATE_SAD
Condiciones Iniciales:
El sistema está en STATE_HAPPY
Se espera que el usuario presione button_a
Eventos generados:
Se presiona button_a.was_pressed()
Resultados esperados:
El sistema muestra la imagen Image.SAD.
El estado cambia a STATE_SAD.
Se reinicia el temporizador con SAD_INTERVAL = 2000 ms.
Resultados obtenidos:
Al presionar el botón A la pantalla cambia a Image.SAD y el estado a STATE_SAD, el vector de prueba funciona

###Vector de Prueba 3: Transición automatica de STATE_SAD a STATE_HAPPY
Condiciones Iniciales:
El sistema está en STATE_SAD
No se presiona ningún botón
Eventos generados:
Se deja pasar el tiempo sin intervención del usuario
Después de SAD_INTERVAL = 2000 ms, el sistema debería cambiar a STATE_HAPPY
Resultados esperados:
El sistema muestra la imagen Image.HAPPY
El estado cambia a STATE_HAPPY
Se reinicia el temporizador con HAPPY_INTERVAL = 1500 ms
Resultados Obtenidos:
Después de 2 segundos vuelve a STATE_HAPPY, el vector de prueba si funciona




