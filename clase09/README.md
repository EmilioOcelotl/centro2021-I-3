# Clase 9

En esta clase vamos a ejercitar la manipulación de imágenes con Processing. 

En específico, trataremos con pixeles e imágenes previamente fijadas. 

Para entender un poco qué pasa con la manipulación de imágenes a través de pixeles, primero vamos a hacer una pequeña prueba.

Por favor, envíen el resultado de estas manipulaciones por correo, serán consideradas para la segunda evaluación. 

Antes que nada, una breve discusión.

## ¿Qué es un glitch? 

En el contexto de las computadoras 

¿Qué es un glitch?

¿Qué es el error?

Un ejemplo de glitch-art y video relativamente controlado: 

[kangding ray // these are my rivers](https://www.youtube.com/watch?v=w-Q4qzeuV-8)

## Imagen como sonido. Databending con programas para editar audio. 

¿Qué es databending?

Consiste en manipular un archivo multimedia de cierto formato, utilizando software diseñado para editar archivos de otro tipo o formato. 

El resultado de esta manipulación es una distorsión que puede incluirse dentro de ala categoría, glitch art. 

Para esta ocasión vamos a utilizar un programa de audio para manipular imagen.

Si bien se pueden utilizar otros programas como adobe audition, en esta ocasión usaremos Audacity.

Audacity es software libre y puede descargarse para cualquier sistema operativo. Se puede descargar en: 

[Audacity](https://www.audacityteam.org/download/)

Una vez que tenemos Audacity instalado en nuestra computadora, tenemos que realizar los siguientes pasos.

### Paso 1: seleccionar una imagen y convertirla

El primer paso consiste en seleccionar una imagen. Para el databending es necesario utilizar formatos sin compresión. Entonces, vamos a seleccionar una imagen de internet o de nuestra computadora y la convertiremos a .bmp o .tif. Para realizar esto utilizaremos algún programa como Photoshop o, siguiendo en el espíritu del software libre, GIMP. 

También es posible utilizar convertidores en línea

[Convertidor en línea](https://www.audacityteam.org/download/)

Una vez que tenemos una imagen en un formato sin compresión vamos a abrirla con Audacity

### Abrir una imagen con Audacity

Para abrir una imagen con Audacity, debemos abrirla con File > Import > Raw Data. Posteriormente a esto, debemos elegir el archivo en cuestión. 

Después nos saldrá una ventana que debemos llenar con la siguiente información: 

- Encoding: U-Law

- Byte order: Big-endian

- Channels: 1 Channel (Mono) 

Una vez realizado esto, damos click en import. 

### Imagen como sonido

Presionen play si se atreven. Lo que estamos haciendo es forzar a Audacity a leer archivos de imagen como si fueran archivos de audio. 

Nota importante: Toda la manipulación que hagamos a continuación debe realizarse cinco segundos después y antes de que inicia el archivo. Esto debido a que el archivo tiene headers o secuencias de información al inicio y al final del archivo que le indican a la computadora cómo leer el archivo (y otras cosas, como los metadatos). 

Entonces, para iniciar, seleccionamos una parte del audio (teniendo en cuenta la nota anterior) la cortamos y la pegamos en otro lado

Hacemos esto repetidas veces en distintas partes del archivo. 

Una vez que ya hemos hecho modificaciones en nuestro archivo, lo exportamos

### Exportar el resultado

Para exportar el archivo: File > Export. Elegimos la ruta para guardar el archivo pero todavía no presionamos save o guardar. 

Vamos a tener que cambiar la configuración de exportación.

Entonces cambiamos el formato del archivo a Other Uncompressed Files y damos click en el botón de opciones. 

Tenemos que cambiar las opciones para que queden de la siguiente manera: 

- Header: RAW (header-less)

- Encoding: U-Law 

Damos guardar no sin antes asegurarnos que la extensión sea la misma que la del archivo original, por ejemplo .bmp. 

Ignoramos la advertencia que arroja Audacity y abrimos el archivo para ver el resultado. 

### Efectos

Audacity cuenta con distintos efectos que es posible agregar a la selección del archivo. Probemos con echo. 

### Conclusiones

Con esta práctica podemos ver que es posible manipular una secuencia unidimensional de datos, en este caso representados en un eje dentro del programa Audacity. 

Las manipulaciones las realizamos en una sola dimensión y esto tiene consecuencias en la manera en que se dibuja la imagen en dos dimensiones (X, Y).

## Glitch-art con Processing

Con lo revisado anteriormente, tanto de clases previas como con lo de databending, es posible deducir un tipo de manipulación tipo glitch en Processing. 

Para realizar esto trabajaremos en un archivo desde cero que será el código de segunda entrega. 

Entonces lo que realizaremos será lo siguiente: 

- Escribir un solo color en pantalla con manipulación de pixeles. 

- Realizar un gradiente. 

- Gradientes cruzados. 

- Leer una imagen

- Manipular los colores de la imagen con un contadores y módulos. Limitar la evolución del desfase de color. 

## Recursos

La práctica de manipulación de imagen con Audacity está basada en el artículo de Antonio Roberts aka hellocatfood-

[Databending using Audacity](https://www.hellocatfood.com/databending-using-audacity/) 
