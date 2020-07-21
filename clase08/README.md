# Clase 8

Premisa de esta parte del curso: hacer filtros para procesar imágenes. 

Cada filtro que hagamos será una clase. 

El día de hoy veremos algunos elementos extras que podemos utilizar con PImage.

Continuaremos con el ejercicio que realizamos la clase pasada.

Trataremos de hacer un primer filtro para la colección de filtros que usaremos.

Con transformaciones podríamos agregar algunas modificaciones a la imagen que procesaremos

Empezaremos a hablar de lectura y escritura de pixeles.

De esta manera, nuestra imagen podrá interactuar con imagenes creadas y transformadas a partir de la lectura y escritura de pixeles. 

Vamos a ver algunos objetos extras que nos servirán para transformar pixeles

## Antes de iniciar: Dibujar figuras con máscaras

Es posible dibujar figuras con el relleno de una imagen. Para realizar esto es necesario hacer una máscara con PGraphics. No hemos visto este objeto y provisionalmente solo lo mencionaremos para resolver el problema.

Hay formas más elegantes de realizar esto que nos pueden servir para hacer mapping. Mostrar un ejemplo de mapping y mostrar el mapeo del CMM. 

A continuación el código que realiza esto:

```java
PGraphics mask;
PImage img;
void setup(){
  size(500,500);

  img=loadImage("screen001.png");
  img.resize(500,500);
  background(255);
  
  mask=createGraphics(width,height);//dibujar el objeto máscara
  
  mask.beginDraw();
  mask.background(0); // fondo
  mask.fill(255); // 
  mask.ellipse(width/2,height/2, 250, 250);
  mask.endDraw();
 
 
  img.mask(mask);
  image(img,0,0);
}
```

## Imágenes Pixeles

Una imagen digital está compuesta por datos. Estos datos son números que indican variaciones de RGB en un punto específico de la cuadrícula de pixeles que compone la imagen. 

Desde nuestra perspectiva, vemos los pixeles dibujados en la pantalla de la computadora como rectángulos minúsculos que están puestos unos tras otros. 

La clase pasada hicimos un pequeño ejercicio para ver la manera en la que se pueden comportar los pixeles con un generador de colores aleatorio. En este ejercicio, representamos un pixel con un cuadrado que se desplegaba en la pantalla. 

A partir de ahora, vamos a vincular el pensamiento creativo con la manipulación de pixeles de bajo nivel a través de Processing. 

Hasta el momento hemos dibujado formas simples y hemos desplegado imágenes que ya existen en pantalla. A partir de hoy vamos a trabajar en torno al dibujo con processing a través de pixeles. 

## PImage 

La clase pasada vimos como desplegar imágenes con PImage. Utilizamos otras funciones como loadImage para cargar la imagen e image para dibujarla. 

Un breve paréntesis: la función loadImage funciona como un Constructor que instancia el objeto PImage 

Esta función realiza el trabajo de un constructor, ya que regresa una nueva instancia del objeto PImage generado a partir de un nombre de archivo. 
Para cargar una imagen tuvimos que desplazarla de su lugar en el disco duro a la carpeta del proyecto en Processing. 

```java
PImage img;

void setup() {
  size(320,240);
  img = loadImage("archivo.extensión");
}

void draw() {
  background(0);
  image(img,0,0);
}
```

Nota importante: La ruta al archivo puede sustituirse por un string. De esta manera podemos cambiar de manera dinámica el archivo que estamos modificando. 

En este sentido podemos agregar un void mousePressed() fuera de draw para que el cambio se realice solamente una vez y no en cada vuelta del draw(). 

Este void mousePressed() funcionará como un bloque de código aparte de setup() y draw() pero en relación a ellos. 

```java
PImage img;                                                                                                                                        
String ruta;  
String ruta2;
int value = 0;
                                                                                                                                                   
void setup() {                                                                                                                                     
  size(540, 540);                                                                                                                                   
  ruta = "algorave1.png";  
  ruta2 = "orbitBlur.png";                                                                                                                      
  img = loadImage(ruta);   
  value = 4; 

}                                                                                                                                                  
                                                                                                                                                   
void draw() {    
  
  
  background(0);                                                                                                                            
  image(img, 0, 0, img.width/value, img.height/value);
}                                                                                                                                                
                                                                                                                                                  
void mousePressed() {                                                                                                                                                                                                                                                                   
  img = loadImage(ruta);
  value = 4;
}

void mouseReleased() {                                                                                                                                                                                                                                                                   
  img = loadImage(ruta2);
  value = 2;
}
```

La primer transformación que hicimos implicó a la función tint() que trabaja de manera muy similar a fill(). Con tint() podemos teñir una imagen existente. 

Entonces, dibujamos la misma imagen en otra posición con valores RGBA en tint(). Esto generó un primer efecto que funciona como una máscara de transparencia. 

```java

PImage img; 
int contador; 

void setup(){
size(960, 540);                                                                                                                                    
img = loadImage("orbitBlur.png");
// blendMode(SUBTRACT);

}

void draw(){
background(255);                                                                                                                                   
//tint(255, 100);
contador= contador + 1;
if(contador == 160){
  contador = contador * -1; 
}
tint(255);                                                                                                                            
image(img, 0, 0, img.width/2, img.height/2);                                                                                                       
tint(202, 255, 0, 124);                                                                                                                            
image(img, abs(contador)-80, 0, img.width/2, img.height/2);                                                                                                   
tint(255, 201, 0, 124);                                                                                                                            
image(img, abs(contador) * -1 +80 , 0, img.width/2, img.height/2);
}


```

## Primer filtro empaquetado como una clase

Teniendo en cuenta esta situación, podemos empezar a empaquetar el funcionamiento de nuestro primer filtro en una clase. 

Recordemos que primero debemos detectar el comportamiento que tiene para definir atributos y funcionamiento interno

### Pixeles

Recordemos que las imágenes son una colección de valores RGB que se almacenan en algún archivo y que se dibujan en pantalla siguiendo la lógica del origen en 0, 0 y del tamaño de la pantalla a lo ancho y a lo alto. 

Recordemos el ejercicio que hicimos la clase pasada, donde un cuadrado representaba un pixel en nuestro canvas.

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

## Para la próxima clase

Vamos a hacer nuestro propio Tint(), trabajaremos en torno a una premisa y estableceremos los principios de la segunda entrega, que se realizará dentro de dos semanas pero que trabajaremos en clase. 

Si avanzamos lo suficientemente rápido no será necesario realizar el ejercicio fuera de clase. 
