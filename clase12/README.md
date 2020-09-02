Audio, imagen y síntesis
Audio, imagen y síntesis. 

En esta clase estaremos revisando la lectura de archivos de audio previamente grabados. 

A diferencia de la síntesis de audio, la reproducción de muestras previamente realizadas nos permitirá aprovechar la complejidad armónica de los sonidos. 

De igual forma podemos aproximarnos a técnicas de composición sonora que nos permitan explorar la perspectiva macro (grabación completa) y la perspectiva micro (extractos ) del sonido. 

Entonces, para cargar y reproducir sonidos en Processing utilizaremos la librería que previamente ya hemos cargado -> Sound

Recordemos que para instalar una librería debemos dar clic en Sketch > Importar Biblioteca > Añadir Biblioteca. 

Una vez en el gestor de bibliotecas, deberán escribir en la casilla de búsqueda “Sound” y deberán seleccionar la única biblioteca que tiene este nombre. Podrán instalar la biblioteca si dan clic en Instalar.

Si instalamos la librería correctamente, la siguiente línea de código podrá ejecutarse sin errores en un sketch en blanco de processing

```java
import processing.sound.*;
```

De hecho, esta línea del programa será la primera de nuestro programa.

El siguiente ámbito que debemos declarar es el de las variables. Primero debemos declarar el objeto que nos permitirá cargar un archivo de audio.

```java
SoundFile miSonido;
```

La clase SoundFile heredará características a miSonido. mi Sonido será el objeto que utilizaremos. 

miSonido funcionará de manera similar a el objeto que creamos cuando utilizamos PImage. En algún momento de nuestro programa debemos guardar el archivo de audio en el objeto para utilizarlo o transformarlo. Este proceso lo podemos hacer setup si no queremos cambiar el archivo en el tiempo.

```java
void setup(){

  size(1000, 800);

  miSonido = new SoundFile(this, "miArchivo.aiff");

}
```

En este caso “miArchivo,aiff” es el nombre del archivo que utilizaremos. Este archivo de audio se comportará de manera muy similar a las imágenes, esto quiere decir que deberemos copiar el archivo que queremos utilizar a la carpeta data (por defecto no existe, deberán crearla) o podremos arrastrar el archivo a la ventana de Processing (con esta modalidad se creará automáticamente la carpeta data).

Por favor usen muestras de sonido que estén en formato .aiff o .wav

Entonces ya podemos usar la instancia miSonido.

Antes de iniciar la transformación de miSonido, es importante describir las características sonoras de una muestra de sonido digital. 

De manera similar a las ondas (por ejemplo, una onda sinusoidal), podemos controlar la amplitud de nuestro sonido, donde 1 es el valor máximo y 0 es la ausencia total de sonido. 

También podemos controlar la altura (que tan agudo o que tan grave es).. La diferencia con respecto a las ondas sintéticas es que vamos a controlar la velocidad (rate) del archivo en un margen que no estará dado en frecuencia, sino en una magnitud que empezará en 1 (velocidad de reproducción normal). 

Un valor de 0.5 reproducirá la muestra a la mitad de su velocidad. En este caso, la velocidad de reproducción y la altura percibida disminuirán. No podremos transformar alguna de las dos por separado (por lo menos con técnicas sencillas de reproducción). 

Más adelante veremos cómo es posible utilizar esto como un recurso estético. 

Para cambiar la velocidad de reproducción utilizaremos el método rate:

```java
miSonido.rate(1); 
```

Podríamos, por ejemplo, utilizar la posición del mouse para cambiar el rango de velocidad. Es importante mencionar que en esta librería no podemos usar números negativos, esto quiere decir que cualquier valor que queramos utilizar para controlar la velocidad de una muestra deberá ser positivo y mayor que 0. 

```java
velocidad = map(mouseX, 0.0, width, 0.01, 4.0);
```

y podríamos sustituir esta variable por el parámetro de velocidad. 

```java
miSonido.rate(velocidad)
```

Es importante mencionar que velocidad deberá ser una variable declarada al inicio del programa. 

Para dar un poco de variación al proyecto, podríamos agregar un mousePressed para que el sonido vuelva a reproducirse cada que presionemos el botón del mouse. Esto nos va a permitir usar mousePressed como un disparador del sonido. En este caso, podríamos usar un sonido corto para que el efecto fuera más interesante. 

```java
void mousePressed(){

   miSonido.play();

}
```

Finalmente, para tener algún otro parámetro, podríamos asociar la amplitud a mouseY como en ejercicios pasados.

```java
amplitud = map(mouseY, 0.0, height, 0.01, 0.8);
```

La operación map transforma un valor de entrada a valores de salida. Este valor es una variable que podemos nombrar como amplitud y que podemos escribir al inicio del programa. 

Con estos elementos podemos construir un programa sencillo que nos permita reproducir muestras a distintas velocidades y con distintas amplitudes cada que presionemos el botón del mouse. 

En el apartado de actividades podrán encontrar el código con una muestra sencilla. El objetivo final de esto es que puedan utilizar este ejemplo y desarrollarlo en términos de  muestras. formas, repeticiones y colores. 

En la próxima sesión aclararemos dudas y comentarios.