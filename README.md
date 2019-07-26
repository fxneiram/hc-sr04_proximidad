# hc-sr04 Sensor de Proximidad
## Esquemático
![alt text](https://github.com/fxneiram/hc-sr04_proximidad/blob/master/Sketch_esquem%C3%A1tico.png)
## Montaje
![alt text](https://github.com/fxneiram/hc-sr04_proximidad/blob/master/Sketch_bb.png)
## Código
```c
const int Trigger = 2;   //Pin digital 2 para el Trigger del sensor
const int Echo = 3;   //Pin digital 3 para el Echo del sensor

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  pinMode(13, OUTPUT); 
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  digitalWrite(13, LOW);
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros
  
  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  if(d<=9){
    digitalWrite(13, HIGH);
  }else{
    digitalWrite(13, LOW);
  }
  Serial.print("cm");
  Serial.println();
  delay(100);          //Hacemos una pausa de 100ms
}


```
