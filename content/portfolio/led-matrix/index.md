---
image: "/ledmatrix/1.jpeg"
title: "Animated LED Matrix"
type: "gallery"
clickablePhotos: true
maxWidth: "800x"
url: "/ledmatrix"
---

### source code

```java
int ledPin = 3;
int ledPin2 = 5;
int ledPin3 = 6;
int ledPin4 = 9;
int ledPin5 = 10;
int ledPin6 = 11;

int delayTime = 10;
int fadeSpeed = 5;

void setup() {
  
}

void loop() {
  delay (30);
  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
    analogWrite(ledPin, brighten);
    delay(delayTime);
  }

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
        analogWrite(ledPin2, brighten);
    }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin, fade);
    delay(delayTime);
  }

 for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
      analogWrite(ledPin3, brighten);
  }
 
   for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
     analogWrite(ledPin2, fade);
     delay(delayTime);
  }

 for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
      analogWrite(ledPin4, brighten);
  }


 for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
     analogWrite(ledPin3, fade);
     delay(delayTime);
 }

 for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
      analogWrite(ledPin5, brighten);
  }

 for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
     analogWrite(ledPin4, fade);
     delay(delayTime);
  }

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
      analogWrite(ledPin6, brighten);
  }

 for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
     analogWrite(ledPin5, fade);
     delay(delayTime);
  }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
     analogWrite(ledPin6, fade);
     delay(delayTime);
  }
  
 // go back

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
    analogWrite(ledPin6, brighten);
    delay(delayTime);
  }

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
        analogWrite(ledPin5, brighten);
    }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin6, fade);
    delay(delayTime);
  }

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
        analogWrite(ledPin4, brighten);
    }

   for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin5, fade);
    delay(delayTime);
  }

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
        analogWrite(ledPin3, brighten);
   }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin4, fade);
    delay(delayTime);
  }

  for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
        analogWrite(ledPin2, brighten);
   }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin3, fade);
    delay(delayTime);
  }

 for (int brighten = 0 ; brighten <= 255; brighten += fadeSpeed) {
        analogWrite(ledPin, brighten);
   }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin2, fade);
    delay(delayTime);
  }

  for (int fade = 255 ; fade >= 0; fade -= fadeSpeed) {
    analogWrite(ledPin, fade);
    delay(delayTime);
  }
 
}

```
