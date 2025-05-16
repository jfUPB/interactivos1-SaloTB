# Vectores de prueba
1. Configuracion del temporizador (A y B)
Objetivo: Asegurar que los botones A y B incrementan y decrementan el temporizador correctamente
Esperado:
El temporizador sube los segundos presionados 
Luego baja los segundos presionados 
"displayText" debe mostrar el texto correpsondiente
Resultado esperado: La pantalla debe mostrar el tiempo ajustado correctamente

Armado de la bomba (S)
Objetivo: Comprobar que la bomba cambia de estado a ARMED al presionar S
Esperado:
Al presionar "S" en la app:
La bomba cambia de estado a STATE_ARMED
El temporizador comienza la cuenta regresiva
"displayText" debe cambiar al texto sorrespondiente, mostrando el tiempo restante
Resultado esperado: La bomba debe armarse y el tiempo debe empezar a contar hacia atras

Desarmado exitoso (A, B, A, S)
Objetivo: Verificar que la secuencia correcta (A → B → A → S) desarma la bomba
Esperado:
El estado vuelve a STATE_CONFIG
displayText cambia al texto correspondiente
El temporizador se resetea a 20 segundos
Resultado esperado: La bomba debe desarmarse correctamente al ingresar la secuencia exacta

Error en la secuencia de desarmado
Objetivo: Asegurar que ingresar una secuencia incorrecta no desarma la bomba
Esperado:
inputSequence se reinicia
La bomba no se desarma
La cuenta regresiva sigue corriendo
Resultado esperado: La bomba sigue armada y la cuenta regresiva continua

Explosion y reinicio con T
Objetivo: Comprobar que la bomba explota al llegar a 0 y que puede reiniciarse con T
Esperado:
La bomba muestra el texto correspondiente al llegar a 0
Al presionar T, vuelve a STATE_CONFIG.
"displayText" regresa al texto correspondiente
Resultado esperado: La bomba explota al llegar a 0, pero puede reiniciarse

Control desde el micro:bit
Objetivo: Comprobar que la bomba también puede controlarse desde el micro:bit.
Esperado:
El comportamiento debe ser igual al de los botones de ya establecidos en P5.js
Resultado esperado: Los controles directos del micro:bit funcionan igual que los botones en la app
