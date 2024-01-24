# P5_dht11_ultrasonico_lcd
## INTRODUCCION

### DESCRIPCION 

La **Esp32**  es un dispositivo electronico en el cual podemos realizar practicas y simulaciones, en esta practica realizaremos un proyecto el cual nos permita visualizar  los valores de distancia, temperatura y humedad. Cabe aclarar que para esta practica se usara un simulador llamado **https://wokwi.com/**.

### MATERIAL A OCUPAR

Para realizar esta practica ocuparemos lo siguente:

-WORKI

-Tarjeta ESP 32

-Sensor DHT-22

-Sensor ultrasonico

-LCD 16x2 (I2C)

### Requisitos previos

Para poder realizar esta practica es nesesario contar con conosimientos basicos de programacion.

## INSTRUCIOES DE ELAVORACION 

1.Abrir la terminal de programación y colocar la siguente programación:



#include "DHTesp.h"

#include <LiquidCrystal_I2C.h>

#define I2C_ADDR 0x27

#define LCD_COLUMNS 20

#define LCD_LINES 4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor

const int Echo = 2;   //Pin digital 3 para el Echo del sensor

void setup() {

Serial.begin(115200);

dhtSensor.setup(DHT_PIN, DHTesp::DHT22);

lcd.init();

lcd.backlight();

  pinMode(Trigger, OUTPUT); //pin como salida
  
  pinMode(Echo, INPUT);  //pin como entrada
  
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  
  lcd.init();
  
  lcd.backlight();

}

void loop() {

TempAndHumidity data = dhtSensor.getTempAndHumidity();

Serial.println("Temp: " + String(data.temperature, 1) + "°C");

Serial.println("Humidity: " + String(data.humidity, 1) + "%");

Serial.println("---");

long t; //timepo que demora en llegar el eco

long d; //distancia en centimetros

digitalWrite(Trigger, HIGH);

delayMicroseconds(10);          //Enviamos un pulso de 10us

digitalWrite(Trigger, LOW);
  
t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso

d = t/59; 

lcd.setCursor(0, 0);

lcd.print(" Temp: " + String(data.temperature, 1) + "\xDF"+"C ");

lcd.setCursor(0, 1);

lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");

lcd.print("Wokwi Online IoT");

delay(2000);

lcd.clear();

lcd.setCursor(0,0);

lcd.print("Dis:"+ String(d) + " CM ");

delay(2000);

delay(1000);

}

2. Se agregan las siguientes librerias para el correcto funcionamiendto del software:
 ![](https://github.com/nijs17/P5_dht11_ultrasonico_lcd/blob/main/q1.png)

3. Hacer las conexiones de la tarjeta con los demas elementos, anteriormente mensionados, como se muestra en la siguente imagen. 

![](https://github.com/nijs17/P5_dht11_ultrasonico_lcd/blob/main/q2.png)

## INSTRUCCIONES DE OPERACION 


    1. Iniciar simulador.
    
    2. Visualizar los datos en el display.
    
    3. Colocar la distancia de trabajao, temperatura y humedad deceadas
    
## RESUSLTADOS
Cuando haya funcionado, verás los valores  se mostraran dentro de display como se muestra en la sigiente imagen.
![]()
