# Pixeles

Recordemos que las imágenes son una colección de valores RGB que se almacenan en algún archivo y que se dibujan en pantalla siguiendo la lógica del origen en 0, 0 y del tamaño de la pantalla a lo ancho y a lo alto. 

Recordemos el ejercicio que hicimos en una clase pasada, donde un cuadrado representaba un pixel en nuestro canvas.

Los pixeles se almacenan como una colección consecutiva de valores que se imprimen en pantalla como si dieran un salto. 

El siguiente ejemplo establece el valor en RGB de cada pixel en la pantalla aleatoriamente en una escala de grises.

```java
// primero establecemos el tamaño de la ventana
// si multiplicamos el ancho por el alto tenemos la cantidad total de pixeles de nuestro canvas
// de todas formas, esto lo podemos obtener con pixels.length
size(400, 400);
// Antes de modificar los pixeles
loadPixels();
// Este loopea para modificar los valores de cada pixel. 
for (int i = 0; i < pixels.length; i++) {
  // rand es una variable que en cada vuelta del draw() tiene un valor aleatorio que va de 0 a 255 en escala de grieses
  float rand = random(255);
  // luego creamos un color que es resultado del número aleatorio que generamos en la escala de grises. 
  color c = color(rand);
  // Establece cada uno de los pixeles dependiendo de su localización (i) al color aleatorio
  pixels[i] = c;
}
// When we are finished dealing with pixels
updatePixels(); 
```

Notemos que primero debemos indicarle a Processing que vamos a trabajar con pixeles. Esto se realiza con las siguientes funciones: 

- loadPixels().- Esta función se invoca antes de acceder al arreglo de pixeles. 

- updatePixels().- Esta función se invoca después de que terminamos de trabajar con los pixeles. 

Si corremos este ejemplo en la relación setup() draw() podemos observar el ejemplo de los cuadrados representando pixeles en una situación real de pixeles.

Si bien estamos determinando la posición de los pixeles con un for(), en el ejemplo que hicimos resulta un poco irrelevante la posición de los pixeles ya que el valor de cada uno de ellos se genera de manera aleatoria. 

Sin embargo, en muchas aplicaciones del procesamiento de imágenes, la posición en X y Y de los pixeles es información crucial. 

Entonces, es importante saber que la posición en X y Y de los pixeles puede ayudarnos a dibujar cosas interesantes.

```java
size(750, 600);
loadPixels();
// Para loopear en cada columna de pixeles 
for (int x = 0; x < width; x++) {
  // Para loopear en cada fila de pixeles
  for (int y = 0; y < height; y++) {
    // Con esta operación encontramos la posición de los pixeles en el contexto de una dimensión 
    int loc = x + y * width;
    if (x % 10 == 0) { // Se colorea de blanco cada 10 columnas de pixeles
      pixels[loc] = color(255);
    } else {          // De lo contrario cambia el color en un gradiente en escala de grises
      pixels[loc] = color(x%255);
    }
  }
}

updatePixels();
```
Notemos que hay una operación que realizamos para saber en qué columna o fila se encuentra un pixel dada.

En la programación con pixeles necesitamos pensar que cada pixel existe en un mundo bidimensional, para acceder a este pixel, es necesario pensar los datos como si estuviera en uno. 

La operación que realizamos para identificar la posición de los pixeles es: 

1. Asumamos que tenemos una ventana o imagen con un ancho y alto determinado.

2. Entonces pensemos que el arreglo de números tiene un número total de elementos que es igual a ancho * alto

3. Para cualquier punto dado X, Y en la ventana, la localización del arreglo de pixeles unidimensional es: posición = x + (y * w)

Pequeño ejercicio: en una imagen de 5x5 ¿cuál sería la posición en X y Y del pixel número 13? Identificarlo con la operación y gráficamente. 

Notemos que el uso de dos for() o la técnica de los for() anidados que hemos utilizado hasta el momento es la forma de escribir en los pixeles. 

La diferencia reside en que dejaremos de pensar los for() anidados para dibujar objetos en dos dimensiones para acceder a los pixeles que existen en un arreglo unidimensional pero que se expresan o dibujan en uno bidimenesional. 

Con esta aproximación a la imagen, además de escribir pixeles también podemos leerlos. 

```java
PImage img;

void setup() {
  size(1274, 1199); // si width tiene un tamaño diferente a la imagen luego se pachequea. 
  img = loadImage("rototecnia.jpeg"); // cargar una imagen 
}

void draw() {
  // Queremos utilizar pixeles
  loadPixels(); 
  // Y también queremos acceder a los pixeles de la imagen que ya cargamos
  img.loadPixels(); 
  
  for (int y = 0; y < height; y++) { // for para Y
    for (int x = 0; x < width; x++) { // for para Y
      int loc = x + y*width; // la operación que requerimos para leer la posición de cada pixel en nuestro arreglo de pixeles
      
      // las funciones red(), green(), y blue() obtienen los tres componentes de color de cada pixel que tiene una posición determinada. 
      float r = red(img.pixels[loc]);
      float g = green(img.pixels[loc]);
      float b = blue(img.pixels[loc]);
      
      // En esta parte del código se realizará el procesamiento de imagen. 
      // esto quiere decir que si queremos cambiar los valores RGB, lo vamos a hacer aquí.
      // antes de colocar al pixel en la ventana 
      
      // En esta parte del código igualamos los pixeles de la imagen y sus respectivos valores en RGB a los pixeles de la pantalla
       pixels[loc] =  color(r,g,b);          
    }
  }
  updatePixels();
}
```

Podemos iniciar el procesamiento de nuestra imagen con un filtro: 

```java
PImage img;

void setup() {
  size(1274, 1199); 
  img = loadImage("rototecnia.jpeg"); 
}

void draw() {
  loadPixels(); 
  img.loadPixels(); 
  
  for (int y = 0; y < height; y++) { 
    for (int x = 0; x < width; x++) { 
      int loc = x + y*width; 
      
      float r = red(img.pixels[loc]);
      float g = green(img.pixels[loc]);
      float b = blue(img.pixels[loc]);
      
     if(r > 100) {
       pixels[loc] = color(r,g,b);
    } else {
      pixels[loc] = color(255);
    }
	//pixels[loc] =  color(r,g,b);          
    }
  }
  updatePixels();
}
```