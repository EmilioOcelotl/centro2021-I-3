# Recursos para la tercera entrega


En las siguientes ligas pueden encontrar recursos suficientes para realizar la tercer entrega. 

Como la mayor parte del código ya está dado, deberán mostrar alguna variación en el draw() de Processing. (formas, colores, posiciones). 

## SuperCollider

El código de SuperCollider es el más sencillo, simplmente hay que declarar en orden de aparición. 

```

p = ProxySpace.push (s.boot); // prende el proxy y corre el servidor

~miSonido2 = {arg freq = 400, amp = 0.5; SinOsc.ar(freq, 0, amp * 0.5)};
~miSonido2.play // para correr el sintetizador
~miSonido2.set(\freq, 500, \amp, 0) // para detener el sonido sin detener el sintetizador

OSCdef(\hola, {arg msg; msg.postln; msg[1].postln; ~miSonido2.set(\freq, msg[1] * 10, \amp, msg[3] / 2)}, "/test", nil)

//OSCdef(\hola).free; // para liberar el sintetizador

NetAddr.langPort; // Esta línea arroja el puerto que está utilizando SC. Deberán sustituirlo en Processing si no es 57120


```

En caso de que la comunicación no funcione (fue el caso de algunas computadoras en clase) Es necesario declarar la última línea para conocer el puerto que está leyendo SC. 

Este número deberá sustituirse por los códigos que aparecen en el setup de Processing. 

## Processing

El código de Processing ya está casi terminado entonces deberán agregar funcionalidades al apartado de draw()


```java
import oscP5.*; 
import netP5.*;

// variables

OscP5 mensaje; // enviar los mensajes OSC desde Processing
NetAddress direccion; // dirección y puerto 
int contador; 

void setup(){
  size(800, 650); 
  mensaje = new OscP5(this, 57120); // el puerto de SC. Si Es diferente en SC deberán cambiarlo
  direccion = new NetAddress("127.0.0.1", 57120);
                             // localhost
}

void draw(){ 

// Deberán realizar algún tipo de modificación aquí. 
  
}

void mousePressed(){
  OscMessage miMensaje = new OscMessage("/test"); // identificador
  miMensaje.add(mouseX); 
  miMensaje.add(mouseY);
  miMensaje.add(0.5); // encendido  
  mensaje.send(miMensaje, direccion); 
}

void mouseReleased(){
  OscMessage miMensaje = new OscMessage("/test"); // identificador
  miMensaje.add(mouseX); 
  miMensaje.add(mouseY);
  miMensaje.add(0); // apagado 
  mensaje.send(miMensaje, direccion); 
}
```

Recuerden que es necesario instalar la librería oscP5 para correr el código
