# El Servidor (Node.js)

## ¿Por qué crees que es útil usar módulos o librerías en lugar de escribir todo desde cero? ¿Qué ventajas aporta? 
Porque asi se ahorra tiempo y se puede mantener un codigo mas ordenado, al tener librerias no es necesario realizar tu mismo el codigo desde cero lo que agiliza el proceso y permite que el codigo no quede tan cragado.

## Experimenta
1. sale el siguiente mensaje en la pagina y no se ejecuta correctamente: Cannot GET /page1.html. Esto pasa porque al cambiar el codigo se esta buscando una carpeta no existente lo que genera el porblema en el servidor "error 404" no se puede encontrar/acceder.
2. Al ejecutarlo de nuevo sin reiniciar la consola el error seguira ocurriendo pues sigue en la misma ejecucion (loq ue no pasaria con los otros archivos qu epueda solicitar el cliente) para que funcione de nuevo se necesita detener y volver a inciar el programa.

##  Rutas: ¿Qué enviar cuando se pide una URL?
1. al tratar de ejecutar la direccion de page1 no se logra encontrar y sale el mismo error 404
2. al utilizar la direccion pagina_uno se logra abriri el vinculo y este funciona correctamente
Esto evidencia que para el servidor pedir la url necesaria para la ejecucion se necesita tener en cuenta su nombre o no se podra ejecutar la funcion asociada

## ¡La Magia de Socket.IO! La Conexión
1. se ve un mensja en la consola el cual intepreto como el ID: M7QK1d3UtxPFriSCAAAJ
2. El ID de la segunda pagina es completamente diferente: jmcttOyihRsnVJmHAAAL
3. Cuando se recargan las paginas o se cierran y se vulevne a abrir los ID cambian por completo para ambas paginas

## Escuchando Mensajes de los Clientes
Ahora se puee ver en la consola la informacion como: el ID de cada una de las pagnias y cuando estas se mueven la informacion de su posicion de forma constante tomando x, y, width y height. Ademas cuando se mueve la pagina uno se resive la informaicon de 
win1update y cuando se mueve la dos se ve info de win2update. (pero ambas resiven el msimo tipo de informacion lo que cambia es de la pagina de la que lo estan resiviendo) 

A la hora de eliminar el broadcast nada cambio a la hora de la recepcion de daton ni de la primera ni segunda pagina. Creo que no se genera ningun cambio porque la funcion de brodcast es envair esta infromacion de cmabio a Todos los demas clientes, y al eleminarlo limito el envio
a la consola, por eos no se vio afectado en la consola, pero si se e4stuviera viendo desde otro punto puede que is se hubiese visto afectada la informacion que estaba llegando

## Poner en marcha el Servidor
Al cmabiar le puerto de incio del ser5vidor sale el mensaje: Server is listening on http://localhost:3001. Al intentar abrir el 3000 este si funciona, pero al abrir el 3001 este tiene el error: no disponible. El 3000 es el puerto de coneccion del computador por lo que si este se cambia no
hay forma de que la coneccion funcione pues no hya un puerto 3001 que se este escuchando.
