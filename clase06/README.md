# Clase 6

## Objetivos

La clase se dividirá en dos partes: La primera será una revisión rápida del funcionamiento de las clases y constructores. La segunda parte consistirá en ejercicios prácticos para aclarar dudas de cara a la entrega de la siguiente semana. 

## Clases y constructores (por fin) 

### Estructura y sintaxis de una clase

Hasta el momento hemos abordado tres nociones: objeto, método y atributo. 

Vamos a agregar un concepto más: clase

Una clase define un grupo de métodos (funciones) y campos/atributos. Si bien podría parecer que un objeto y una clase son similares, tienen diferencias. 

Estas diferencias tienen que ver con la manera en la que se estructuran comportamientos y atributos en la POO. 

Importante: Un objeto es una instancia simple de una clase. 

Entonces, podemos complejizar el ejercicio de la analogía entre objeto, método y atributo.

Por ejemplo clase radio, con el atributo radio frecuencia y el método asignar frecuencia. 

Una instancia de esa clase, es decir un objeto, podría ser radio FM (87.5 -108 Mhz) y radio de onda corta (3 -30 Mhz) 

Otro atributo podría ser el color de la radio, no solamente la radio frecuencia

### Ejemplo de cómo se usa una clase y ejercicio de hacer una clase

Cuando definimos una clase creamos nuestro propio tipo de tipos de datos. 

Ya hemos visto que existen tipos de formas de almacenar datos en Processing como: int, float y boolean. 

En ocasiones hablamos un poco de objetos y revisamos String, una clase para empezar a trabajar con series de caracteres. 

Definir una clase es parecido a este último tipo de datos: es posible almacenar variables y métodos dentro de un mismo nombre. 

Para crear una clase primero debemos tener claro qué queremos que haga el código. 

En este sentido, es común que primero hagamos la lista de variables que requeriremos (estos serán los campos o atributos). 

El nombre de una clase es importante: Los nombres de las clases siguen las mismas convenciones que las variables (¿Cuáles?). 

Los nombres de las clases siempre deben ir en mayúsculas. 

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

A continuación, el ejemplo que desarrollamos la clase pasada en relación a una clase. 

```java
Circulo cir; 

void setup() {
  size(600, 600); 
  cir = new Circulo();
  cir.x = width/4; 
  cir.y = height/4;
  cir.d = 0;
}

void draw() {
  background(0);
  noStroke(); 

  cir.d = cir.d + 1;

  if (cir.d > 120) {
    cir.d = cir.d * -1;
  }
  
  for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
      int paso = i + 1; 
      int paso2 = j + 1; 
      ellipse(cir.x*paso, cir.y*paso2, cir.d, cir.d); 
    }
  }
}

class Circulo {
  float x, y; 
  float d;
}
```

### Constructores

Un constructor es un bloque de código que se activa al mismo tiempo de que se crea un objeto. 

Los constructores siempre tienen el mismo nombre que la clase y se usan por lo general para asignar valores a los campos de un objeto al mismo tiempo que se crean. 

Si no hay constructor en una clase, entonces los valores de cada campo númerico se inicializan en cero.

El constructor es igual que otros métodos. La única diferencia que tiene es que no está precedido por la definición de un tipo de tado (int, boolean etc) ni por la palabra void. 

A continuación, la implementación de un constructor en el código que hasta el momento hemos escrito. 

```java
Circulo cir; 

int x = 10;
int y = 4; 
int diaLim = 40;

void setup() {
  size(600, 600); 
  cir = new Circulo(x, y, 0);
}

void draw() {
  
  background(0);
  noStroke(); 

  cir.d = cir.d + 1;
  
  if (cir.d > diaLim) {
    cir.d = cir.d * -1;  
  }
  
  for (int i = 0; i < x -1; i++) {
    for (int j = 0; j < y -1; j++) {
      int paso = i + 1; 
      int paso2 = j + 1; 
      ellipse(cir.x*paso, cir.y*paso2, cir.d, cir.d); 
    }
  }
}

class Circulo {
  float x, y, d;
  
  Circulo(float xpos, float ypos, float dia){
    x = width/xpos;
    y = height/ypos;
    d = dia; 
  }
  
}
```

También podemos utilizar métodos dentro de la misma clase que nos puedan ayudar a resolver ciertas tareas.

El siguiente código utiliza lo que hemos visto hasta el momento y lo traslada al interior de la clase.

```java
// Paso 1: declarar el objeto
// Importante señalar que este objeto está en relación con el último bloque de código que es la declaración de la clase
// Una clase es la definición de un tipo de objeto
// Un objeto es la realización o la instancia de una calse

Circulos cir; 

void setup() {
  size(600, 600); 
  
  // Construir el Objeto
  // Cantidad de Círculos en X, Cantidad de Círculos en Y, Límite del diámetro; 

  cir = new Circulos(2, 8, 200); 
}

void draw() {

  background(0);
  noStroke(); 

  // Para dibujar nuestros círculos
  // El método dibujarCirculos dibujará el arreglo con las características determinadas arriba
  
  cir.dibujarCirculos(); 
  
  // Nuestro objeto tiene otro método: imprimirValores

  cir.imprimirValores(); 

}

// Aquí es donde escribimos la clase

class Circulos {
  
  // Lo primero es determinar qué valores influyen en nuestra clase:
  // cantidad de cículos en x, cantidad de círculos en y, diámetro y límite del diámetro
  // Los cuatro valores son números de punto flotante, entonces pueden declararse todos a la vez
  
  float x, y, d, dLim;
  
  // Luego viene el constructor
  // El constructor es una especie de puente de comunicación entre el funcionamiento de la clase
  // y las características delimitadas al inicio del programa o trasformados a lo largo del mismo
  // En este caso, el constructor de la clase Círculos tiene 3 parámetros
  // Omitimos el valor del díametro ya que este cambia dinámicamente y está delimitado por diaLim

  Circulos(float xpos, float ypos, float diaLim) {

    // Tenemos que igualar los valores del constructor a las variables que declaramos arriba
    
    x = xpos;
    y = ypos;
    dLim = diaLim;
    
  }

  // Posteriormente declaramos el primer método que dibuja los círculos con un comportamiento dado

  void dibujarCirculos() {
 
    // utilizamos las variables declaradas al inicio de la clase
    
    d = d + 1;

    if (d > dLim) {
      d = d * -1;
    }

    // estas partes del código ya las habíamos dibujado anteriormente
    // Para este caso, lo que estamos haciendo es sustituir en algunos casos nombres de variables anteriormente designadas
    // Por los nombres de las variables que declaramos en la clase
    
    for (int i = 0; i < x; i++) {
      for (int j = 0; j < y; j++) {
        ellipse((width/(x+1))*(i+1), (height/(y+1))*(j+1), d, d);
      }
    }
    
  }
  
  // Podemos tener los métodos que queramos
  // En este caso, el metodo imprime valores imprimirá una cadena de caracteres que arrojará información sobre
  // el comportamiento del programa. 
  // al final, cuando invocamos el método imprimir valores, realmente estamos haciendo uso de un código "empaquetado"
  
  void imprimirValores (){
      println("Círculos en X: " + x + ", Cículos en Y: " + y + ", Círculos totales: " + (x * y) + ", Valor del diámetro: " + abs(d));
  }
  
}
```

## Ejercicios en clase para la primera entrega

- Debe tener setup() y draw().

- Debe hacer uso de la condicional if(), por lo menos en su versión más básica.

- Debe de contar con la estructura for() de forma tal que puedan demostrar las posibilidades de la repetición y el dibujo de formas.

- Debe incluir un contador que cambie dinámicamente algún parámetro (tamaño, color o posición) de las figuras dibujadas.

- Debe incluir comentarios que expliquen el funcionamiento del programa

Adicionalmente, el ejercicio puede contar con:

- La incorporación de strings o cadenas de caracteres y su dibujo en pantalla por medio de la función text().

- El uso de arreglos de datos de cualquier tipo, idealmente, de strings para complementar el punto anterior.

- Utilizar las formas más complejas de la condicional if/else.
