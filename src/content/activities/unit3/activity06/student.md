# Vectores de prueba
## Limite de A y B, tiempo maximo y minimo
Lo esperado: Al oprimir el boton A el contador sumara 1 a la cuenta regresiva de la bomba, y dejara de sumar al llegar al tiempo maximo, en este caso 60
Lo esperado: Al oprimir el boton B el contador restara 1 a la cuenta regresiva de la bvomba, y dejara de restar al llegar al tiempo minimo asignado, en este caso 10
Lo esperado: Al cambiar el Maximo y el minimo de los limites de la bomba el contador debera de adecuarse a estos nuevos limites

La prueba fue exitosa

## Resive el codigo de desactivacion tanto desde el puerto serial como del micro:bit 
Lo esperado: Utilizando unicamente los comandos del púerto serial en el orden de desactivacion establecido debe llevarlo de nuevo a estado configuracion
Lo esperaod: Utilizando unicamente los botones del micro:bit en el orden de desactivacion establecido debe llevarlo de nuevo a estado configuracion
Lo esperado: Ya que el porgrama no deberia de diferenciar entre los botones del micro:bit y los del puerto serial el codigo usando la combinacion de ambos deberia de funcionar por igual
Lo esperado: Al ingresar la secuencia incorrecta la bomba no se desactivara

La prueba fue exitosa

## Volver a estado configuracion desde el boton touch y la T del puerto serial
Lo esperado: Al oprimir el boton touch debera de volver a estado configuracion
Lo esperado: Al oprimir la T desde el puerto serial debera volver a estado configuracion
Lo esperado: Al orpimir la T o el boton touch del micro:bit en medio de otro estado que no sea Explocion, no sucedera nada

La prueba fue exitosa

