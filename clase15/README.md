
# SuperCollider y Processing por medio de OSC

## Repaso

La clase pasada vimos como enviar mensajes OSC en una red local. 

Conectarse a una red común (con o sin conexión a la red) es el primer paso para enviar mensajes. 

Posteriormente debemos buscar la dirección IP de la computadora a la que queremos enviar mensajes. 

En SuperCollider esto puede ser no necesario, lo que más importa para el envío de mensajes OSC en una red es el puerto

Por defecto, SuperCollider utiliza el puerto 57120. 

Processing, por otro lado, utiliza 12000

Estos valores pueden personalizarse. 

Una vez que tenemos la dirección IP y el puerto, podemos enviar mensajes OSC.

Utilizamos las clases `NetAddr` y `OSCFunc` para registrar estos parámetros. 

Cuando igualamos NetAddr a una variable, podemos acceder a sus métodos. Entonces NetAddr.sendMsg permite que enviemos mensajes OSC. 

La sintaxis para enviar mensajes OSC es sencilla, primero debemos escribir el identificador del mensaje. Este es una palabra o letra antecedida de una diagonal. 

`/test`

Los identificadores son sensibles a mayúsculas. 

Posteriormente separamos el identificador del mensaje por medio de una coma. 

En caso de que queramos enviar más de un mensaje, los separamos con comas. 

## Comunicación local 

Premisa: hacer un sintetizador controlado por un sketch en Processing. 

La clase pasada vimos que es posible comunicar mensajes entre computadoras conectadas a una red. 

El día de hoy vamos a ver que es posible realizar el intercambio de mensajes de OSC entre aplicaciones dentro de una misma computadora. 

Vamos a hacer el ejercicio más sencillo: Cada que demos clic en la pantalla comunicaremos un mensaje OSC con las coordenadas en X y Y del mouse. 

Por defecto Processing no utiliza clases para enviar/recibir OSC, así que lo primero que tenemos que hacer es instalar la librería oscP5.

Esto lo podemos hacer con el gestor de paquetes de Processing. 

Luego vamos a preparar el sketch de Processing. 

```java
import oscP5.*;
import netP5.*;
  
OscP5 oscP5;
NetAddress myRemoteLocation;

void setup() {
  size(400,400);
  frameRate(25); // reducimos el frameRate para que no sea tan costoso. 
  oscP5 = new OscP5(this, 56120); // para enviar a supercollider
  myRemoteLocation = new NetAddress("127.0.0.1", 56120);
}

void draw() {
  background(0);
}

void mousePressed() {
  OscMessage myMessage = new OscMessage("/test");
  myMessage.add(mouseX);
  myMessage.add(mouseY); 
  oscP5.send(myMessage, myRemoteLocation); 
}
```


Entonces del lado de SuperCollider hay que hacer un lector de estos mensajes:

```java
n = NetAddr("127.0.0.1", 57120)

OSCFunc({ arg msg, time, addr, recvPort; 
	[msg, addr].postln; 
}, "/test", n);

```

Luego podemos construir algunos sintetizadores para hacer esto un poco más interesante:

Por ejemplo podríamos jugar con los arreglos y el estéreo. 

También podríamos introducir a la síntesis extractiva y explicar la síntesis aditiva. 

Al final podríamos agregar un amp para prender/apagar el sintetizador cada que reciba un mensaje. 

```java
p = ProxySpace.push(s.boot)
s.meter
~algo = {arg freq = 100, tic = 2, amp = 1; Pan2.ar(SinOsc.ar(freq*2, 0, 0.5) * Impulse.kr(tic)) * amp}
~algo = {arg freq = 100, tic = 2, amp = 1; Pan2.ar(Ringz.ar(WhiteNoise.ar(0.5) , freq, 0.05))* Impulse.kr(tic) * amp}
~algo.play
```

Entonces del lado de Processing podríamos agregar algunas funciones para que interactúen con el sintetizador. 

Por ejemplo: 

```java
import oscP5.*;
import netP5.*;
float rand = 0;
float rand2 = 0;

OscP5 oscP5;
NetAddress myRemoteLocation;

void setup() {
  size(400,400);
  //frameRate(25); // reducimos el frameRate para que no sea tan costoso. 
  oscP5 = new OscP5(this, 57120);
  myRemoteLocation = new NetAddress("127.0.0.1", 57120);
}

void draw() {
  
  if(mousePressed){

    rand += random(-6, 6);
    rand2 += random(-6, 6);
    ellipse(mouseX + rand, mouseY + rand2, 20, 20);
  } else {
    rand = 0;
    rand2 = 0;
  }
  
}

void mousePressed() {
  float mapeo = map(mouseY, 0, width, 1, 60);
  frameRate(mapeo); 
  OscMessage myMessage = new OscMessage("/test");
  myMessage.add(mouseX);
  myMessage.add(mouseY); 
  myMessage.add(1);
  oscP5.send(myMessage, myRemoteLocation); 
}

void mouseReleased() {
  OscMessage myMessage = new OscMessage("/test");
  myMessage.add(0);
  myMessage.add(0); 
  myMessage.add(0);
  oscP5.send(myMessage, myRemoteLocation); 
}
```

Como ejercicio final podríamos hacer una especie de ejercicio interconectado. Entonces, la idea es que traigan manipulaciones del código de Procesing y de SuperCollider para que podamos interactuar. 
