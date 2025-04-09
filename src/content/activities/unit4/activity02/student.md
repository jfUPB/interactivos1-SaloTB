
## Explicación

### #1
Tras declarar las variasbles locales se crea la funcion preload

    function preload() {
      lineModule[1] = loadImage('data/02.svg');
      lineModule[2] = loadImage('data/03.svg');
      lineModule[3] = loadImage('data/04.svg');
      lineModule[4] = loadImage('data/05.svg');
    }
preload() carga las imagenes SVG antes de que comience el programa para usarlas como pinceles

### #2

Se establecen las propiedades del pincel, el tamaño del lienzo y su color

    function setup() {
      createCanvas(windowWidth, windowHeight); // Crea un lienzo del tamaño de la ventana
      background(255); // Fondo blanco
      noCursor(); // Oculta el cursor
      strokeWeight(0.75); // Grosor de línea del pincel
      c = color(181, 157, 0); // Color inicial del pincel
    }


### #3

El tamaño del lienzo se ajusta a la pantalla

    function windowResized() {
      resizeCanvas(windowWidth, windowHeight);
    }

### #4
    function draw() {
      if (mouseIsPressed && mouseButton == LEFT) {
        var x = mouseX;
        var y = mouseY;
        if (keyIsPressed && keyCode == SHIFT) {
          if (abs(clickPosX - x) > abs(clickPosY - y)) {
            y = clickPosY;
          } else {
            x = clickPosX;
          }
        }
    
        push();
        translate(x, y);
        rotate(radians(angle));
    
        if (lineModuleIndex != 0) {
          tint(c); 
          image(lineModule[lineModuleIndex], 0, 0, lineModuleSize, lineModuleSize);
        } else {
          stroke(c);
          line(0, 0, lineModuleSize, lineModuleSize);
        }
    
        angle += angleSpeed;
        pop();
      }
    }

Determina la posicion del mause en "y" y "x"
Si se prime shift limita la direccion de las lineas a horizontales
guarda el estado actual con push()
Determina el angulo del pincel y lo aumenta 
si existe un modulo SVG seleciconaod lo dibuja con "imagen" si no solo dibuja una linea
Restaura el estado con pop()

### #6
    function mousePressed() {
      lineModuleSize = random(50, 160); // Genera un tamaño aleatorio del pincel
      clickPosX = mouseX; // Guarda la posición del clic en X
      clickPosY = mouseY; // Guarda la posición del clic en Y
    }
Al hacer click el tamaño del mause cambia de forma aleatoria

### #7
Con las flechas se puede variar la velocidad de rotacion y el tamaño del pincel

    function keyPressed() {
      if (keyCode == UP_ARROW) lineModuleSize += 5;
      if (keyCode == DOWN_ARROW) lineModuleSize -= 5;
      if (keyCode == LEFT_ARROW) angleSpeed -= 0.5;
      if (keyCode == RIGHT_ARROW) angleSpeed += 0.5;
    }

### #8
    function keyReleased() {
      if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
      if (keyCode == DELETE || keyCode == BACKSPACE) background(255);
    
      if (key == 'd' || key == 'D') {
        angle += 180;
        angleSpeed *= -1;
      }
    
      if (key == ' ') c = color(random(255), random(255), random(255), random(80, 100));
    
      if (key == '1') c = color(181, 157, 0);
      if (key == '2') c = color(0, 130, 164);
      if (key == '3') c = color(87, 35, 129);
      if (key == '4') c = color(197, 0, 123);
    
      if (key == '5') lineModuleIndex = 0;
      if (key == '6') lineModuleIndex = 1;
      if (key == '7') lineModuleIndex = 2;
      if (key == '8') lineModuleIndex = 3;
      if (key == '9') lineModuleIndex = 4;
    }
Esta parte genera varios cambios a las lineas y sus angulos: si oprimes el espacio cambia el color de forma aleatoria, si oprimers d invierte la rotacion del angulo, si se oprime de 1 a 4 cambia el color (no aleatoriamente) y si se oprime de 5 a 9 cambia el tipo de píncel SGV. Finalmente si se oprime la "S" se guarda una imagen en PNG.

## Imagenes
Esta la cree cambiando tanto el pincel SVG (con los numeros 5 a 9) como el color (con los numero de 1 a 4) mientras oprimia constantemente el mause.
![250402_82555_588](https://github.com/user-attachments/assets/09d065a8-75b8-42b7-b4b2-dec822fb8bba)

Esta imagen la cree moviendo el mause por la pantalla mientras cambaiba de forma aleatoria y simultanea el SVG utilizado y el color del pincel, al igual que la rotacion del angulo oprimiendo "d"
![250402_82753_172](https://github.com/user-attachments/assets/cdf7f6c1-dd9c-453d-bc29-1de7fc97bb65)


