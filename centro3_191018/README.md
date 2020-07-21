
# Clase 10

En esta sesión realizaremos los últimos ejercicios de pixeles e imágenes. 

Hasta el momento hemos dibujado pixeles y patrones directamente en la pantalla. 

También leímos imágenes y las manipulamos con funciones nativas de Processing. 

Posteriormente aprendimos a leerlas y dibujarlas directamente de funciones de lectura de pixeles. 

Manipulamos linealmente un arreglo de pixeles en Audacity. Esta transformación tuvo consecuencias en la imagen que se dibujó en dos dimensiones. 

Con esta idea desplazamos el color de los pixeles de una imagen para hacer transformaciones tipo glitch-art. 

En esta ocasión aprenderemos a leer la cámara que por defecto está integrada en nuestra computadora. 

Realizaremos algunas transformaciones en los pixeles de la cámara para completar nuestro filtro de Processing. 

Pero antes de eso, algunas sugerencias para el ejercicio que realizaremos como entrega. 

## Sugerencias

- Lo más importante: comentar el código. 

- Anclar las manipulaciones a caracteres del teclado, así podemos tener distintos filtros con distintas transformaciones en la imagen. El ejercicio debe tener al menos dos combinaciones de teclas con manipulaciones distintas. 

- Estas manipulaciones pueden ivolucrar: 

  1) la lectura de una imagen con image() y loadImage() y su manipulación con tint() 
  2) la escritura de pixeles directamente en pantalla 
  3) la lectura de una imagen con pixeles y la manipulación de los canales de color, 
  4) El desfase de los parámetros de color y posición con contadores
  5) y finalmente, la manipulación de cámara/video
  
Entonces, idealmente la entrega se centra en la manipulación de una imagen previamente cargada. A continuación revisaremos la lectura de la cámara y de videos previamente cargados. 

## Introducción: librerías y extensiones

Las funciones nativas de Processing nos permiten realizar dibujos con formas sencillas. 

Hay diversos paquetes que permiten extender las posibilidades de Processing. Estos paquetes se llaman librerías y por lo general atienden a premisas específicas. 

Podemos acceder al repositorio de extensiones oficiales de Processing de la siguiente manera: 

Sketch > importar biblioteca > añadir biblioteca

Para leer la cámara o videos en Procesing es necesario instalar y cargar una biblioteca. 

En la pestaña de buscar escribimos video y colocamos el cursor en la biblioteca Video. Con el botón install agregamos la biblioteca a Processing. 

## Lectura de la cámara

Para cargar la biblioteca en nuestro programa, debemos agregar la siguiente línea en la parte superior de nuestro código. 

```java
import processing.video.*;
```

De manera similar a las variables, las bibliotecas deben cargarse al inicio del programa. 

Con el siguiente código agregamos una instancia para capturar video. 

```java
Capture cam
```

En `setup()` es necesario declarar la nueva instancia de nuestra variable que captura video e iniciarla. 

```java
cam = new Capture(this, Capture.list()[0]);
cam.start();
```

`Capture.list()` nos arrojará una lista con las cámaras que están disposibles en nuestra computadora.

Si tenemos más de una cámara conectada o integradaa a la computadora, podemos acceder a ellas con un arreglo. 

En caso de que solamente tengamos la cámara integrada, casi siempre es posible acceder a ella con el primer índice de la lista. 

De esta manera, `Capture.list()[0]` "cargará" la primer cámara que encuentre, por lo general la integrada. 

En caso de que haya un problema, es necesario leer qué dispositivos están conectados con `println()`

Si salen errores extraños, una posible solución se encuentra en: 

[Solución a posible error con la cámara](https://github.com/gohai/processing-video/releases/tag/v1.0.2)

Con el siguiente código leemos los pixeles de la cámara (en caso de que haya una, en todo caso el if() puede ser innecesario). 

```java
  if (cam.available() == true) {
    cam.read();
  }
```

Posteriormente hay que leer los pixeles como lo haríamos con cualquier imagen 

```java
  cam.loadPixels();
```

Finalmente accedemos a cada uno de ellos como si fueran una imagen con `cam.pixels[loc]`

## Video

Leer un video funciona de manera similar. A continuación el código para cargar y desplegar un video

```java
import processing.video.*;

Movie movie;

void setup() {
  size(640, 360);
  background(0);
  movie = new Movie(this, "transit.mov");
  movie.loop();
}


void draw() {
  if (movie.available() == true) {
    movie.read(); 
  }
  image(movie, 0, 0, width, height);
}
```

Entonces, para leer los pixeles de un video (y transformarlos) podemos usar el siguiente código: 

```java


import processing.video.*;

Movie movie;

void setup() {
  size(640, 360);
  background(0);
  movie = new Movie(this, "transit.mov");
  movie.loop();
}


void draw() {
  if (movie.available() == true) {
    movie.read(); 
  }
  //image(movie, 0, 0, width, height);
  loadPixels();
  movie.loadPixels();
  for(int x = 0; x < width; x++){
    for(int y = 0; y < height; y++){
      int loc = x + y * width;
      float red = red(movie.pixels[loc]);
      float green = green(movie.pixels[loc]);
      float blue = blue(movie.pixels[loc]);
      pixels[loc] = color(red, green, blue); 
    }
  }
  updatePixels();
}
```

## keypressed y key

Finalmente para hacer nuestro selector de escenas vamos a utilizar `ìf()`, `keyPressed` y `key`

El siguiente ejemplo da cuenta del funcionamiento de keyPressed y key

```java
void setup(){
}

void draw(){
if(keyPressed){
  if(key == 'a'){
    println("Se imprimió una a");
  }
  
   if(key == 'b'){
    println("Se imprimió una b");
  }
}
}
```

Con este último código tenemos elementos suficientes para realizar la segunda entrega. 
