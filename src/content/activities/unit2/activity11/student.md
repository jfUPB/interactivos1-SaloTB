# Diseño de la Lógica de una Bomba Temporizada
![Mapa conceptual sencillo](https://github.com/user-attachments/assets/57b5f206-d037-4669-85ec-c9800939fdca)

Se espera que el funcionamiento de este codigo sea el siguiente: primero se detrminaran los estados y el tiempo incial del prograna, luego
se determinaran los puntos maximos a los que la bomba puede modificarse. Tras tener todo nombrado se pasara a la creacion de cad auno de los
estados por su propia cuenta inciando por estado configuarion, este estado no se cambiara a menos de que la condicion "shake" sea nombrada y
por ende el usuario podra manipularla sin tiempo predefinido oprimiendo el boton "a" para añadir tiempo y el boton "b" para disminuirlo hasta 
los limites previamente establecidos. Esta suma y resta que se ira mostrando en el micro:bit se almacenara en una variable "countdown_time"
que servira para determinar los segundos en el segundo estado Estate_Armed, el cual tendra la capacidad de contar el tiempo transcurrido para 
luego restarle ese mismo tiempo al ya mensionado "countdown_time" (Esto haciendo la convercion de milisengundos a segundos). Siendo el caso de
que el tiempo transcurrido sea igual a 0 se pasara al ultimo estado Estate_Exploded, donde se mostrara la imagen de una calavera y se hara sonar 
un sonido que indique que la bomba estallo. Finalmente en este mismo estado se tendra una condicion para determinar si el sensor en el micro:bit 
es precionado, lo que hara que se devuelva al Estate:Configuracion, donde se podra reinciar el proceso y por ende la bomba.
