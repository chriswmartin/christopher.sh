---
title: "Beginner Arduino Tutorials"
draft: false
showDate: false
showWords: false
---

![](/posts/images/arduino.jpeg)

### Buttons & LEDS 
```java
int led1 = 8;
int led2 = 9;

int buttonPin = 2; 
int buttonState = 0;

int delaytime = 100;

void setup() {
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);

  pinMode(buttonPin, INPUT);

  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  
  if (buttonState == 0) {
    digitalWrite(led1, HIGH);
    delay(delaytime);
    digitalWrite(led2, HIGH);

    digitalWrite(led1, LOW);
    delay(delaytime);
    digitalWrite(led2, LOW);
  }
}
```

### Photocells
```java
int photocellPin = 0;
int photocellReading;
int ledPin;
int brightness;

void setup() {
  ledPin = 11;
    pinMode(ledPin, OUTPUT);

  Serial.begin(9600);  
}

void loop() {
  photocellReading = analogRead(photocellPin);  
 
  Serial.print("Analog reading = ");
  Serial.println(photocellReading);

  brightness = map(photocellReading, 10, 100, 0, 255);

  analogWrite(ledPin, brightness);
 
  delay(100);
}
```

### Ultrasonic Sensors
```java
int triggerPin = 9;
int echoPin = 8;
int threshold = 100;
int duration;
int distance;
int previousDistance;

void setup() {
  pinMode(triggerPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}
void loop() {
  previousDistance = distance;
  
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);

  digitalWrite(triggerPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration*0.034/2;

if (previousDistance < (distance - threshold) || previousDistance > (distance + threshold)){ 
  Serial.println("Large change in distance");  
}

Serial.print("Distance: ");
Serial.println(distance);

delay(100);
}
```

### Servos, Buttons, & Potentiometers
```java
#include <Servo.h>

Servo myservo;
int potpin = 0;
int value;
int buttonPin = 3;
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT);
  myservo.attach(8);

  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);
  
  value = analogRead(potpin);
  value = map(value, 0, 1023, 0, 180);
  myservo.write(value);
  Serial.print(" ");

  Serial.print(value);
  delay(100);

Serial.print(buttonState);
  if (buttonState == 0) {
    myservo.write(180);
  }
   if (buttonState == 1) {
    myservo.write(0);
  }

}
```
