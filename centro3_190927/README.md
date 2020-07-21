# Clase 7

Strings, Matrices, algo de arreglos. 

Clase y objeto > explicación con manzanas. 

Con estas posibilidades hemos manejado tipos de datos que ya conocíamos y los hemos puesto en relación con un nuevo tipo de datos: la cadena de caracteres. 

El día de hoy vamos a revisar PImage para trabajar con imágenes. 

## Nota previa 

Para la próxima entrega (fecha por definir) realizaremos un cargador y procesador de imágenes tipo filtro y lo empaquetaremos en una clase sencilla.

El objetivo final es tener una matriz con distintas instancias de la clase y variaciones de manipulación de la misma imagen. 

Podríamos agregar un modo para que capture imágenes de la cámara. 

Objetivo: entender la imagen digital y su manipulación por medio de Processing. 

## Imágenes en el contexto digital

El fundamento de las fotografías y las imágenes digitales es distinta a las analógicas. 

Las imagenes funcionan de manera similar a la pantalla de la computadora: son rejillas rectangulares de color. 

Las dimensiones de las imagenes se miden en unidades llamadas pixeles, que de hecho es la medida con la que hemos estado trabajando todo este tiempo en Processing. 

Se puede obtener el total de pixeles de una imagen multiplicando la cantidad de pixeles a lo ancho por la cantidad de pixeles de alto. 

Cada imagen digital tiene una profundidad de color. 

La profundidad de color refiere al número de bits usados para almacenar cada pixel. 

Si la profundidad es de uno, entonces se pueden almacenar dos valores de color solamente. 

Si la profundidad de color de una imagen es 8, entonces cada pixel puede tener un valor de hasta 256 valores. 

Entonces: las imágenes digitales están compuestas de series de números que representan colores. 

El formato en el que se almacenan las imágenes determina cómo estos números son almacenados. 

Algunos formatos almacenan los datos de color en arreglos matemáticamente complejos para comprimir los datos y reducir el tamaño del archivo resultante. 

Ahora no nos vamos a detener mucho en los formatos, para el objetivo de lo que realizaremos: Processing puede cargar GIF, JPEG, PNG.

### Ejercicio: matrices y ruido

No es casual que hayamos iniciado por dibujar matrices de dos dimensiones: el prinicipio es básicamente el mismo. 

Si sustituimos las figuras dibujadas por cuadrados continuos podríamos generar una imagen de muy baja definición: por ejemplo de 600 x 600 pixeles. 

Cada uno de los puntos de la matriz es como si fuera un pixel. 

Ejercicio: rejilla de dos dimensiones para dibujar una generador de ruido visual con una definición relativamente baja. 

Premisa: tamaño y profunidad de color.

### Despliegue de imágenes

Processing puede cargar imágenes, desplegarlas en la pantalla, cambiar su tamaño, posición y opacidad. 

Para cargar el tipo de datos de las imágenes es necesario invocar PImage. 

De la misma manera en que los enteros son almacenados en variables con `int`, y los valores `true` y `false` son almacenados en `boolean`, las imágenes pueden almacenarse en variables de PImage. 

Antes de desplegar una imagen primero es necesario cargarlas con la función `loadImage()`

Es necesario agregar la extensión del formato. 

Como vimos con el caso de los archivos .txt, si una ruta no es especificada, es necesario colocar la imagen en la misma carpeta del proyecto. 

```java
image(nombre, x, y);
image(nombre, x, y, width, height);
```

Los parámetros de `image()` determinan la imagen que se va a dibujar, su posición y tamaño. 

```java
size(960, 540);
PImage img;
img = loadImage("screen001.png");
image(img, 0, 0, img.width/2, img.height/2);
```

La función `tint()` puede colorear las imagenes. Es una función que funciona de manera similar a `fill()` y `stroke()` pero afecta solamente a las imágenes. 

Sigue la misma sintaxis para colorear que `fill()` y `stroke()`, esto es, todas las imagenes que se dibujen despues de correr `tint()` se teñirán del color especificado en los parámetros. 

Esto no tiene efectos permantentes en las imágenes, si corremos `noTint()` entonces la coloración de todas las imágenes desaparecerá. 

```java
size(960, 540);
PImage img;
img = loadImage("screen001.png");
tint(100, 255, 100); 
image(img, 0, 0, img.width/2, img.height/2);
```
También es posible aplicar transparencias y teñido a las imágenes. 

```java
size(960, 540);
PImage img;
img = loadImage("screen001.png");
background(255);
//tint(255, 100); 
image(img, 0, 0, img.width/2, img.height/2);
tint(202, 0, 255, 104); 
image(img, -40, -40, img.width/2, img.height/2);
tint(255, 201, 0, 104); 
image(img, 40, 40, img.width/2, img.height/2);
```

Con teñido, transparencias y modificación del color para teñir una imagen podemos tener los primeros pasos para realizar nuestra clase que modifique imagenes. 

Ejercicio extra: dibujar una imagen con transparencia y algún color en el teñido y agregar repeticiones de desplazamiento con for()` en vez de hacerlas mano (como en el ejemplo anterior)
