
# Clase 5 | Práctica de programación orientada a objetos

## Plan

En esta clase realizaremos un ejercicio parecido al de la clase pasada. 

Agregaremos algunas funcionalidades, por ejemplo, determinar con variables el tamaño del arreglo de círculos y el límite del tamaño de los círculos. 

Posteriormente sustituiremos los cículos por textos provenientes de un texto con saltos de línea y relativamente complejo. 

Aprenderemos cómo leer y manipular arreglos de strings, para eso, tendremos que repasar cómo se comportan los arreglos

Finalmente introduciremos algunas ideas sobre las clases en el contexto de la programación orientada a objetos y los constructores. 

De esta manera, trataremos de delimitar el control sobre el ejemplo que vamos utilizando. 

### Arreglos (repaso) 

El término array o arreglo hace referencia al agrupamiento estructurado. En la programación de computadoras, un arreglo es un conjunto de elementos de datos almacenados bajo el mismo nombre. 

Los arreglos pueden ser creados para almacenar cualquier tipo de dato y cada uno de estos elementos pueden ser individualmente asignados y leídos. 

Puede haber arreglos de números, caracteres, strings, valores booleanos etc. 

Los arreglos pueden almacenar datos de vectores de figuras complejas, teclazos recientes del teclado o datos leídos de un archivo. 

Los arreglos pueden ser útiles, por ejemplo, podemos almacenar cinco valores enteros en un solo arreglo de entero más que definir cinco variables separadas. 

Entonces, los arreglos pueden ser útiles para agrupar datos de cualquier tipo. En caso de que estemos usando grandes cantidades de datos, es posible simplicar la tarea de escribir y agrupar datos por medio de arreglos. 

Los elementos de un arreglo se empiezan a contar desde cero. Entonces, el primer elemento está en la posición [0], el segundo en [1] y así sucesivamente. 

Los arreglos se declaran de manera similar a otro tipo de datos y se distinguen por el uso de corchetes: [ y ]. 

Cuando se declara un arreglo, el tipo de dato que almacena debe ser especificado. 

Una vez que el arreglo es creado, sus valores pueden ser asignados. 

A continuación, tres formas de declarar arreglos de números en Processing

```java
int[] data;
void setup() {
size(100, 100);
data = new int[5];
data[0] = 19;
data[1] = 40;
data[2] = 75;
data[3] = 76;
data[4] = 90;
}
```

```java
int[] data = new int[5];
void setup() {
size(100, 100);
data[0] = 19;
data[1] = 40;
data[2] = 75;
data[3] = 76;
data[4] = 90;
}
```

```java
int[] data = { 19, 40, 75, 76, 90 };
void setup() {
size(100, 100);
}
```

### Relación con la clase String

¿Es posible sustituir la posición de los círculos con texto dibujado en pantalla, leído de un archivo txt?

Los siguientes ejemplos que aparecen en el documento de la clase pasada pueden ayudarnos a resolver este problema. 

```java
String[] lines = loadStrings("ohplaces.txt");
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
