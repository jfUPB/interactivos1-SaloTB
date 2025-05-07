## Explorando los clientes (p5.js + Socket.IO)

###  Variables globales y conexión inicial
Al inciar elprograma y abrir la pagina todo funciona correctamente y cuando se desactiva y refresca la pagina aparece el siguiente error de coneccion: No se puede acceder a este sitio localhost rechazó la conexión. Al volverlo a inciar y refrescar la pagina vuelve a la normalidad, ya no hay mas errores
El error indica que no se puede acceder a la pagina, al no estar inciado el servidor no se encuentra a la pagina a la que se quiere acceder y por ende no se encuentra ni accede. 

### Manejando la conexión establecida
Antes de mover la pagina 2 llego a la terminal informacion incial de la pagina 1, la informacion de la pagina 2 en cambio solo llega cuando se mueve, la informacion de la pagina 2 es correcta pero se emite la informacion incial. Esta infromacion incial puede ser util para determinar si la pagina esta funcionando
como deberia de ser antes de cualquier alteracion. 

### Recibiendo datos del servidor
Al mover la ventana page 1 se dispara el log “Page 2 received..." y muestran sus datos en la page 2. Cuando se mueve la ventana 2 sin emabrgo este evento no se dispara, pues el evento esta leyendo los datos enviados por la primera para asi darle esta informacion a la segunda, por lo que en ningun
momento los datos de su propio movimeinto son mostrados en la terminal

###  Detectando cambios y enviando actualizaciones
El mensaje aparece cuando la pagina se mueve, si se deja quieta el mensaje deja de aparecer, el cambio detecta cada movimeinto realizado. Considero que comprar con el dato anterior es util pues asi se puede comparar que tan amplio es el cambio y si este es correcto, ademas al comprarlo se puede 
evidenciar si efectivamente hubo un cambio, pues si no se comprarar podria estar dando constantemente ele mismo dato caundo en realidad no se ha realizado ningun cambio.

### La visualización (draw)
Cambie el tamaño de las lineas y su color, tambien la posicion inicial del circulo, finalmente le cambie el radio al circulo
![image](https://github.com/user-attachments/assets/172dd568-84e0-4f2a-ae7b-385c2222c8cc)
![image](https://github.com/user-attachments/assets/6c3b9052-b7d9-4e8f-8b82-0fb72c9e82fa)
![image](https://github.com/user-attachments/assets/49266960-71c9-448f-b5b9-5f0c5645b10d)

