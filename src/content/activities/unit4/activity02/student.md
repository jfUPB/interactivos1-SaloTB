# Caso de estudio: exploración inicial

## Ejemplo elegico
http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_1_2_03

## Explicación

Al incio se declaran las variables globales 
### #1

    var tileCount = 20; // Numero de diviciones de la cuadricula
    var moduleColor; // Donde se almacena el color de los cuadros
    var moduleAlpha = 180; // Opacidad de los cuadros
    var maxDistance = 500; // Tiene en cuenta la distancia del mause con respecto a los cuadros (Distancia maxima)

### #2

    function setup() { 
      createCanvas(600, 600); // Se crea el lienzo de 600x600
      noFill(); // Evita que los cuadros tengan relleno
      strokeWeight(3); // Determina el grosor de los bordes del cuadro
      moduleColor = color(0, 0, 0, moduleAlpha); // Define el color, en este caso negro con una transparencia de 180
    }
### #3

    function draw() {
      clear(); // Borra el canvas en cada fotograma
      stroke(moduleColor); // Aplica el color a los bordes

### #4
Para la creacion de la rejilla se utiliza un doble ciclo For:

    for (var gridY = 0; gridY < width; gridY += 25) { 
      for (var gridX = 0; gridX < height; gridX += 25) {

Donde Gridx y Gridy representan el tamaño de cada cuadrado. En este caso ademas se llena la pantalla con una dejilla de 25x25 

### #5

    var diameter = dist(mouseX, mouseY, gridX, gridY); // calcula la distancia entre elmause y el cuadro actual
    diameter = diameter / maxDistance * 40; // vuelve el tamaño de los cuadrados a su estado original y delimita su rango con una regla de tres. [0, 40] Teniendo en cuenta que su maxima distancia es 500

El dimetro cambia dependiendo de si el mause esta cerca o lejos del cuadrado, si esta cerca "diameter" es grande, mientras que si esta lejos es pequeño. 
Calcula la distancia euclidiana entre dos puntos utilizando la funcion "dist"

### #6

    push(); //Guarda la transformacion actual
    translate(gridX, gridY, diameter * 5); // mueve el sistema de cordenadas a las posiciones de gridx y gridy, *5 hace referencia a un movimeinto en Z
    rect(0, 0, diameter, diameter); Dibuja un cuadrado con "diameter" como base
    pop(); // Restaura la transformacion anteriormente guardada por push

### #7

    function keyReleased() {
      if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
    }

Finalmente se tiene esta funcion que permite guardar la iomagen actual del canvas al precionar "s"


En resumen este codigo genera una rejilla de cuadros con un diametro determinado que reacciona a la cercania del mause dada por las cordenadas del mismo sobre las cordenadas de cada cuadro. Esto permite que el diametro se altere en los cuadros mas cercanos a la pocision actual de mause y se recuperen volviendo a su tamaño original cuando este mismo de aleja. 
  
