
# Clase 4 | Programación orientada a objetos

Ejemplo de código creativo: Lev Manovich. 

Este autor es un punto de quiebre para considerar como centrales algunas ideas del trabajo con información, la programación y el software. 

En términos analíticos (políticos y sociales) pero también para referir a las implicaciones estéticas del cruce entre arte, ciencia y tecnología. 

Este punto de partida puede articularse con lo que estamos revisando en clase. 

## Ejercicios de repaso

De cara a la primera evaluación, será necesario que realicen ejercicios.

Para que estos ejercicios puedan ser considerados como métodos de evaluación será necesario que tengan los siguientes elementos. 

- Ejercicios dinámicos, esto es, deben utilizar la relación setup() - draw(). 

- Utilizar el loop for() para dibujar una especie de matrix con repeticiones y variaciones de dibujos sencillos. 

- Utilizar al menos una vez la estructura if() else() y métodos de entrada como el teclado o el mouse.

- Lo más importante: Tener en cuenta la relación entre variación y repetición, comentarios en el código que expliquen lo que va sucediendo. 

## Ejercicio para llegar a la creación de clase

String pero también la estructuras que servirán para realizar los ejercicios. Una vez que hayamos resuelto esto iniciaremos con la explicación y realización de clases en Processing. 

### setup() draw() y variables

¿Cómo se estructura esta parte del código? ¿Cuál es la sintaxis?

Realizaremos un ejercicio para que tengamos código que pueda manipularse en la parte de creación de clases. 

```java
void setup(){

}

void draw(){

}
```

Primera parte del ejercicio: Realizar una matrix de 3x3 con círculos del mismo tamaño utilizando solamente width y height como variables reservadas y cambiar dinámicamente el tamaño de todos los círculos. Nota: igualar las posiciones determinadas por width y height a variables, también el diámetro del círculo. 

### Condicionales e interacción con el mouse

¿Cuál es la sintáxis y de qué manera se relacionan if y else? 

Las condicionales funcionan de manera parecida a las preguntas. Permiten a un programa realizar una acción si la respuesta a la pregunta es "cierto" o realizar otra acción si la respuesta es "falso". 

Las preguntas formuladas dentro de un programa son siempre declaraciones lógicas o relacionales. 

En el siguiente ejemplo tenemos el caso de dos condicionales para dos objetos. Si esta condición se cumple, entonces lo que se encuentra dentro de las llaves se ejecuta. Si no se cumple, el código no se ejecuta. 

Este es un caso específico de la estructura if. 

Para el caso de las condicionales del ejemplo ejecutado, hay expresiones relacionales que compara dos valores con un operador relacional. En el ejemplo de arriba, la expresión es "i < 400" y el operador es < (menor que). Los operadores relacionales más comunes son:

| Símbolo | Operación        |
|:-------:|:----------------:|
| >       | Mayor que        | 
| <       | Menor que        |
| >=      | Mayor o igual que|
| <=      | Menor que        |
| ==      | Igual a          |
| !=      | No es igual a    |


```java
x = 90

if (x < 100) {
rect(35, 35, 30, 30);
}

if (x > 100) {
ellipse(50, 50, 36, 36);
}


line(20, 20, 80, 80);

```

Con condicionales podemos agregar otro comportamiento en el tamaño de los círculos. En esto consiste la siguiente parte del ejercicio. 

Utilizando condicionales sencillas ¿cómo podríamos asignarle un comportamiento oscilatorio al tamaño de los círculos? 

¿Qué otros parámetros podríamos modificar? 

### loop for()

En el código que hemos escrito hemos notado regularidades. Estas regularidades pueden simplificarse con el loop for(). 

Si bien hay distintas formas de llegar a un mismo resultado en Processing, es importante tener en cuenta que muchas veces tener un código eficiente nos ayuda a entender rápidamente lo que estamos haciendo y realizar tareas de manera rápida. 

Por ejemplo: 

```java
size(480, 120);
strokeWeight(8);
line(20, 40, 80, 80);
line(80, 40, 140, 80);
line(140, 40, 200, 80);
line(200, 40, 260, 80);
line(260, 40, 320, 80);
line(320, 40, 380, 80);
line(380, 40, 440, 80);
```

Puede simplificarse de la siguiente manera: 

```java
size(480, 120);
strokeWeight(8);
for (int i = 20; i < 400; i += 60) {
line(i, 40, i + 60, 80);
}
```

### Relación con la clase String

¿Es posible sustituir la posición de los círculos con texto dibujado en pantalla, leído de un archivo txt?

Los siguientes ejemplos que aparecen en el documento de la clase pasada pueden ayudarnos a resolver este problema. 

```java
String[] lines = loadStrings("numbers.txt");
for (int i = 0; i < lines.length; i++) {
println(lines[i]);
}
```

split

```java
String s = "a, b";
String[] p = split(s, ", ");
println(p[0]); 
println(p[1]);
```

```java
int paso = 2;

void setup(){
size(600, 600);
// background(0);
String[] lines = loadStrings("ohplaces.txt");

}

void draw(){
  background(0);
  paso = paso + 1;
  //fill(paso);
textSize((paso % 30)+1);

// println(lines[int(random(100))]); 

rectMode(CENTER); // interpreta posX posY como el centro de la figura

text(lines[int(random(100))], width/2, height/2, 80, 80);
text(lines[int(random(100))], width/4, height/4, 80, 80);
text(lines[int(random(100))], width/4*3, height/4*3, 80, 80);

}
```

### Ejercicio en clase /  tarea

Tomar el ejemplo que hasta el momento hemos construido, variar formas, tamaños, colores y comportamientos. Enviarlos por email con comentarios que expliquen cómo funciona. 

## Estructura y sintaxis de una clase

Hasta el momento hemos abordado tres nociones: objeto, método y atributo. 

Vamos a agregar un concepto más: clase

Una clase define un grupo de métodos (funciones) y campos/atributos. Si bien podría parecer que un objeto y una clase son similares, tienen diferencias. 

Estas diferencias tienen que ver con la manera en la que se estructuran comportamientos y atributos en la POO. 

Importante: Un objeto es una instancia simple de una clase. 

Entonces, podemos complejizar el ejercicio de la analogía entre objeto, método y atributo.

Por ejemplo clase radio, con el atributo radio frecuencia y el método asignar frecuencia. 

Una instancia de esa clase, es decir un objeto, podría ser radio FM (87.5 -108 Mhz) y radio de onda corta (3 -30 Mhz) 

Otro atributo podría ser el color de la radio, no solamente la radio frecuencia


## Ejemplo de cómo se usa una clase y ejercicio de hacer una clase


Cuando definimos una clase creamos nuestro propio tipo de tipos de datos. 

Ya hemos visto que existen tipos de formas de almacenar datos en Processing como: int, float y boolean. 

La clase pasada hablamos un poco de objetos y revisamos String, una clase para empezar a trabajar con series de caracteres. 

Definir una clase es parecido a este último tipo de datos: es posible almacenar variables y métodos dentro de un mismo nombre. 

Para crear una clase primero debemos tener claro que queremos que haga el código. 

En este sentido es común que primero hagamos la lista de variables que requeriremos (estos serán los campos o atributos). 

Tener en cuenta las variables que utilizaremos nos ayudará a darnos cuenta de qué tipo serán. 

El nombre de una clase es importante: Los nombres de las clases siguen las mismas convenciones que las variables (¿Cuáles?). 

Sin embargo, los nombres de las clases siempre deben ir en mayúsculas. 

Ya hemos visto un poco de esto con String, esto ayuda a que podamos distinguir a partes del código como String o PImage de los tipos de funciones que se escriben con minúsculas como int o boolean. 

Podemos elegir, por ejemplo el nombre circulo. 

Si consideramos que el ejemplo que hicimos a lo largo de la clase es una función ellipse() entonces los parámetros/campos de nuestra clase pueden seguir la misma lógica

float x - coordenadas del círculo en x

float y - coordenadas del círculo en y

float diameter - diametro del círculo

Una vez que los atributos y el nombre de la clase han sido determinados, hay que considerar cómo el programa se comportará sin el uso de un objeto. 

Para el caso del ejemplo que hemos utilizado, algunos parámetros están definidos en variables, básicamente posición del círculo y diámetro. 

Entonces, traduzcamos el programa que hicimos a la forma de estructurar el código que hemos mencionado hasta el momento

¿Qué pasa? 

Es importante señalar varias cosas: 

La primera es que la clase Circulo no es muy útil hasta el momento, sin embargo es el inicio para ver de qué manera podemos introducir lo que hasta el momento hemos visto. 

Es importante señalar que la clase Circulo y el objeto cir son cosas diferentes. 

Los objetos son creados a partir de una clase y una clase describe un conjunto de campos/atributos y métodos. 

Una instancia de una clase funciona como una variable y como cualquier variable, debe tener un nombre único. 

Si queremos realizar varias instancias de clase, podemos diferenciarlas entre ellas por medio de la declaración de distintos nombres. 

En la próxima clase complejizaremos y trabajaremos en torno a otras cosas, por ejemplo, constructores. 
