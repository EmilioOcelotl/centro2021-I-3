# Clase 3. Introducción a programación orientada a objetos 

Objetivo: Durante esta clase y la siguiente realizaremos un ejercicio de puntillismo con Processing y veremos la forma de traducir este ejercicio a clases. 

## Paradigmas de la programación orientada a objetos

En el siglo XX, el procesamiento de datos han conformado la base de las ciencias de la computación como disciplina. 

La sintaxis y la forma física de la presentación de información ha sido la prioridad en este campo. 

La programación orientada a objetos inició en 1960 con el lenguaje de programación Simula desarrollado por Ole-Johan Dahl y Kristen Nygaard.

En este paradigma, los objetos son los elementos básicos. El software se estructura como una colección de objetos que trabajan juntos. 

El núcleo del paradigma de la programación orientada a objetos: objetos actúan unos sobre los otros a través del envío de mensajes. 

La diferencia entre la programación orientada a objetos y otros paradigmas de programación: en la primera, los datos y las operaciones que manipulan estos datos se encuentran en un mismo objeto, en vez de estar separados. 

La POO se diferencia de la programación procedimental, cuyo comportamiento está definido por procedimientos, funciones y subrutinas. 

En POO, estos comportamientos están contenidos en los métodos de los objetos. 

Un método es una propiedad básica de una case de objeto. Los métodos de los objetos están ocultos en el objeto mismo. 

Los métodos pueden ser invocados al enviar un mensaje adecuado al objeto. 

### Objetos

Variables y funciones son bloques que sirven para construir software. Con frecuencia, algunas funciones se utilizan juntas para trabajar con un grupo de variables relacionadas. 

La programación orientada a objetos fue desarrollada para hacer este proceso más explícito: usa objetos y clases como bloques para construir software. 

Una clase define un grupo de métodos (funciones) y atributos o campos (variables). Un objeto es una instancia simple de una clase. 

Los atributos o campos dentro de los objetos son accesibles por lo general vía sus propios métodos. Esto permite al objeto "ocultar" su complejidad.  

Además de proporcionar un modelo conceptual útil, la programación orientada a objetos se convierte en una necesidad cuando un programa incluye muchos elementos o cuando crece en contenido. 

Los objetos pueden proveer un poderoso medio de pensar y estructurar ideas en el código. Esto también facilita la lectura y procesamiento de datos. 

Todo el software escrito en Processing consiste en objetos, pero este hecho se omite, de forma tal que los conceptos de la programación orientada a objetos pueda ser introducida después. 

### Programación orientada a objetos

Un programa modular está compuesto por módulos de código. Cada módulo realiza una tarea específica. 

Podemos pensar en las variables como el elemento básico para manipular elementos dentro de un programa. Permiten a un solo valor aparecer muchas veces a lo largo del código. También permiten que ese mismo valor pueda cambiar fácilmente. 

Hasta el momento, hemos visto variables que pueden almacenar números o estados booleanos. En algunas ocasiones también hemos visto texto que aparece entre comillas ¿String? 

De manera similar a las variables, las funciones abstraen una posible tarea y permiten usar bloques de código en todo el programa escrito. 

Entonces, nuestro programa puede ser una relación entre tipos de datos que se pueden expresar en variables y funciones que manipulan estos datos.

Típicamente nos preocupamos solamente por lo que la función hace, no por cómo funciona. Esto puede ser problemático: el caso de los automóviles, la computadora, el teléfono. 

¿Estos dispositivos son cajas negras? 

Tipos de cajas negras: registrador de vuelo pero también pueden ser elementos que podemos estudiar en función de las entradas que recibe y las salidas que produce, sin tener noción de cómo funcionan. 

Cuando ciertas cosas del funcionamiento de los objetos permanecen ocultas, nos podemos enfocar en los objetivos del programa y no tanto en la complejidad de su infraestructura. 

## Ejemplo en lenguaje natural

Es posible establecer una analogía entre un objeto en software y artefactos del mundo real. 

Estas analogías nos ayudarán a entender la forma de pensar del mundo de la programación orientada a objetos. 

Atributos: Volumen, frecuencia, banda(AM y FM), encendido/apagado

Métodos: establecerVolumen, establecerFrecuencia, establecerBanda

Siguiendo con esta analogía ¿Cuáles serían los atributos y métodos del objeto automóvil? 

## Método y atributo vs función y variable

A las variables dentro de un objeto se les llama atributos y a las funciones dentro de un objeto se les llama métodos. 

En este sentido, un objeto combina datos relacionados (atributos) con acciones y comportamientos relacionados (métodos). 

En Processing, Métodos y atributos funcionan exactamente como variables y funciones hasta el momento vistas. 

Utilizaremos estos nuevos términos para enfatizar que son parte de un objeto. 

Es posible acceder a los métodos y atributos a través del punto (que funge como operador), un periodo establecido entre el nombre del objeto y el nombre de la función dentro del objeto. 

## Discusión

Problemática de la ilusión de objetividad y la representación de la neutralidad. En ciencias de la computación esto está anclado al funcionamiento y la optimización de los sistemas. 

¿Qué pasa cuando esta aproximación contempla la interacción con seres humanos? 

Una posible crítica a este paradigma tiene que ver con el pre-establecimiento de comportamientos y significados. Desde la perspectiva del diseño de software, esto no deja espacio para la duda o la negociación. 

Como usuarios el que algo esté oculto puede ser problemático.

En este sentido, conocer el paradigma puede ser un punto de partida para cambiar el significado de la interacción "lista para usarse"

Usuarios que tienen la capacidad de desplazarse hacia la programación en todo caso se vuelven expertos en escapar a la interacción planeada y de determinar el uso de los programas en su mundo de interacción. 

En este sentido los programas pueden significar pero también pueden ser significados de difentes maneras. 

Aprender a hacer una clase y entender a través de la práctica este paradigma

### String y tipos de datos. 

Los objetos PImage, PFont y String son tipos de datos y cada uno tiene funciones y elementos de datos adicionales únicos. 

Un objeto es la clase String que veremos a continuación.

## Processing

### Explicación String

Un string es una cadena de caracteres, esto es, una secuencia ordenada y finita de elementos que pertenecen a un cierto tipo de lenguaje formal o alfabeto. 

Así como las variables pueden almacenar números de punto flotante o enteros como tipos de datos, las cadenas de caracteres y los caracteres también son un tipo de dato que Processing puede utilizar. 

En Processing los caracteres siempre se definen dentro de comas simples `'a'` mientras que las cadenas de caracteres se definen dentro de comas dobles `"cadena"`

El ejemplo siguiente muestra cómo funciona `string` y cómo una colección de caracteres se puede convertir en una cadena. 

```java 
String str1 = "cadena";
char data[] = {'c', 'a', 'd', 'e', 'n', 'a'};
String str2 = new String(data);
println(str1);  // Imprime cadena en la consola
println(str2);  // Imprime cadena en la consola
```

String en Processing como un tipo de dato incluye métodos para examinar caracteres individuales en una cadena, extraer partes de la cadena, convertir la cadena de alguna forma (por ejemplo cambiar todos los caracteres a mayúsculas) e incluso comparar dos variables de cadena. 

Métodos que puede recibir string. 

```java
String ejemplo = "Metodos de una cadena"; // primero declaramos la cadena

println(ejemplo.charAt(2)); // para buscar caracteres en un índice específico

if(ejemplo.equals("metodos de una cadena de caracteres")){
  println("Sí, los valores son los mismos");
}
else{
  println("No, los valores no son los mismos");
}

// Imprime el índice de la primera vez que aparece un caracter específico. 

println(ejemplo.indexOf('d')); 

// Número de elementos de la cadena

println(ejemplo.length()); 

// regresa un substring que es parte del string original, 
// pero que está delimitado por un indice inicial y uno final

println(ejemplo.substring(4, 12)); 

// minúsculas

println(ejemplo.toLowerCase());

// mayúsculas

println(ejemplo.toUpperCase());
```

Hasta el momento hemos partido del objeto String para explicar como Processing se aproxima al paradigma de la POO. 

Independientemente de esto y de las implicaciones de que el objeto String cumpla con las características de método y atributo que la relacionan con el paradigma de la POO, hay funciones en Processing que interactúan con string y que pueden darle aplicaciones interesantes a los programas que de alguna manera interactúan con cadenas de caracteres. 

```java
String s = "Próxima sesión: extructura y sintáxis de una clase.";
fill(50);
text(s, 10, 10, 70, 120);

// en este caso estamos determinando: 

// cadena de caracteres
// posicion en X y Y del cuadro que despliega el texto
// ancho y alto del cuadro que determina el texto

// text(str, x1, y1, x2, y2); 
```

Para cargar archivos que pueden ser números, letras, palabras, cualquier cosa que sea representable como texto pero esta vez, en un archivo txt

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
