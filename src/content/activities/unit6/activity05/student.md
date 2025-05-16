## Modificación creativa del caso de estudio

### Idea de modificacion
Para este proyecto me gustaria crear tambien paginas que puedan interactuar entre ellas, algo que me llama mucho la antencion son los puzles por lo que se me ocurrio que una de las paginas pueda actuar como una lupa y las demas paginas parescan vacias, pero al acercar la lupa se puedan ver cosas
en ellas, ademas dependiendo de su tamaño y orientacion lo que estas otras ventanas pueden contener puede ser difernete y esto al final revela una palabra o codigo final si es hehco de forma adecauda. Una de las ventanas da el orden de como se debe de leer la otra, mientras que la otra da
imagenes o letras que se deben organizar en un orden para desifrar algo. (En total son tres paginas) 

### Servidor codigo
    const express = require('express');
    const http = require('http');
    const socketIO = require('socket.io');
    const path = require('path');
    
    const app = express();
    const server = http.createServer(app); 
    const io = socketIO(server); 
    const port = 3000;
    
    // Estado inicial de las dos páginas
    let page1 = { x: 0, y: 0, width: 100, height: 100 };
    let page2 = { x: 0, y: 0, width: 100, height: 100 };
    
    // Servimos archivos desde /views
    app.use(express.static(path.join(__dirname, 'views')));
    
    // Rutas específicas para cada página
    app.get('/page1', (req, res) => {
        res.sendFile(path.join(__dirname, 'views', 'page1.html'));
    });
    
    app.get('/page2', (req, res) => {
        res.sendFile(path.join(__dirname, 'views', 'page2.html'));
    });
    
    // Conexiones por WebSocket
    io.on('connection', (socket) => {
        console.log('Usuario conectado - ID:', socket.id); 
    
        socket.on('disconnect', () => {
            console.log('Usuario desconectado - ID:', socket.id);
        });
    
        socket.on('win1update', (window1, sendid) => {
            console.log(' win1update de ID:', socket.id, '→', window1);
            page1 = window1;
            socket.broadcast.emit('getdata', page1);
        });
    
        socket.on('win2update', (window2, sendid) => {
            console.log('win2update de ID:', socket.id, '→', window2);
            page2 = window2;
            socket.broadcast.emit('getdata', page2);
        });
    });
    
    server.listen(port, () => {
        console.log(`Servidor escuchando en: http://localhost:${port}`);
    });


### Clientes codigo 

#### Lupa
    <!DOCTYPE html>
    <html lang="es">
    <head>
      <meta charset="UTF-8">
      <title>Lupa</title>
    </head>
    <body style="background: white;">
      <h2>Lupa Activa</h2>
      <script>
        let targetWindow;
    
        // Abre la otra ventana cuando se carga
        window.addEventListener('load', () => {
          targetWindow = window.open('/contenido.html', 'contenido', 'width=800,height=600');
        });
    
        // Envía coordenadas del mouse a la ventana de contenido
        document.addEventListener('mousemove', (e) => {
          if (targetWindow) {
            targetWindow.postMessage({ x: e.clientX, y: e.clientY }, '*');
          }
        });
      </script>
    </body>
    </html>
#### Secreto 
    <!DOCTYPE html>
    <html lang="es">
    <head>
      <meta charset="UTF-8">
      <title>Contenido Oculto</title>
      <style>
        body {
          margin: 0;
          overflow: hidden;
          background: #000;
          font-family: monospace;
          color: lime;
          font-size: 18px;
        }
    
        #container {
          position: relative;
          width: 100vw;
          height: 100vh;
          background: #000;
        }
    
        #oculto {
          position: absolute;
          width: 100%;
          height: 100%;
          color: lime;
          background: #000;
          padding: 20px;
          line-height: 1.6;
          mask-image: radial-gradient(circle 100px at -200px -200px, rgba(0, 0, 0, 1) 0%, transparent 100%);
          -webkit-mask-image: radial-gradient(circle 100px at -200px -200px, rgba(0, 0, 0, 1) 0%, transparent 100%);
          z-index: 1;
          pointer-events: none;
        }
    
        .matrix {
          white-space: pre-wrap;
        }
      </style>
    </head>
    <body>
      <div id="container">
        <div id="oculto">
          <div class="matrix">
    01100101 01110011 01110100 01101111 00100000 01100101 01110011 00100000 01110101 01101110 00100000
    01101101 01100101 01101110 01110011 01100001 01101010 01100101 00101100 00100000 01100100 01100101
    01110100 01110010 01100001 01110011 00100000 01100101 01101110 01110100 01110010 01100101 01101100
    01100001 01111010 01100001 01100100 01101111 00100000 01100001 01110000 01101111 01110011 01110100
    01100001 01110011 00100000 01110000 01100001 01110010 01100001 00100000 01110010 01100101 01110110
    01100101 01101100 01100001 01110010 00101110
          </div>
        </div>
      </div>
    
      <script>
        const oculto = document.getElementById('oculto');
    
        // Recibe coordenadas desde la lupa y actualiza la máscara
        window.addEventListener('message', (event) => {
          const { x, y } = event.data;
          oculto.style.webkitMaskImage = `radial-gradient(circle 100px at ${x}px ${y}px, rgba(0, 0, 0, 1) 0%, transparent 100%)`;
          oculto.style.maskImage = `radial-gradient(circle 100px at ${x}px ${y}px, rgba(0, 0, 0, 1) 0%, transparent 100%)`;
        });
      </script>
    </body>
    </html>

### Video
https://www.canva.com/design/DAGnpEXz3Vk/GpYX5_CNhc7b7TBXDvPgvw/edit?utm_content=DAGnpEXz3Vk&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton 
### Final 
Fue especialmente dificl tratar de acoplar una tercera pagina, tuve que limitar mi idea a dos paginas y hacerlo mas similar al ejemplo de coneccion de telefono de la unidad 7 donde con el movimeinto en una de las paginas afectaba la otra, pues la idea original fue demasiado dificil de plasmar. En la realizacion de este proyecto me comence a percatar de como al comunicacion de las paginas funciona gracias a Node.js y socket.io el primero sirviendo mas para la comunicacion directa del servidor y el Socket.io para comunicaciones mas bidireccionales y perosnlaizadas, aunque el codigo como tal no me quedo 100% claro, aun pude entender la logica tras la comunicacion y el "puente" que permiten estas dos herramietnas 
