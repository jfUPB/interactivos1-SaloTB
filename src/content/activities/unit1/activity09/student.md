#### Codigo
let x = 200
let y = 300
let x1 = 100
let y1 = 300
let z1 = 0
let b = 0

function setup() {
  createCanvas(400, 400);
}

function draw() {
  
  x = random(0,400)
  y = random(0, 400)
  x1 = random (200, 400)
  y1= random(100,300)
  z1 = random (0, 400)
  b = random (300,400)
  
  background(b);
  fill('#F1EED4')
  
  fill('#673AB7')
  circle(x, y, 100)
  
  fill('#BA9EEC')
  circle(x1, y1, z1)
  
  fill('#03A9F4')
  circle(x1, y1, z1)
  
}

#### Captura 
![image](https://github.com/user-attachments/assets/3bbd9891-cd1c-4126-9703-f854e41c634d)

#### Explicacion
Utilice las funciones random() despues de definir una variable de las pocisiones en x y y y el diametro del circulo (La figura utilizada) y puse un rango de movimeinto en la msima funcion permitiendo que el objeto
se m,ueva por la pantalla de forma aleatoria y ademas cambie de tamaño. Finalmente agregue esta funcion al fondo para que se reiniciace el cambio de forma aleatoria y para mejorar la distincion entre acda uno de los circulos
les puse un co0lor en especifico a cada uno. 
