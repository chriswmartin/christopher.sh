---
title: "Draw with LEDs using Processing"
draft: false
showDate: false
showWords: false
---

Using computer vision in [Processing](https://processing.org) you can draw on your computer screen using only LEDs and a webcam.

### Source Code 
```java
import processing.video.*;

Capture video;

color trackRed; 
color trackGreen; 
color trackBlue;
int threshold = 50;

ArrayList<PVector> redPoints = new ArrayList();
ArrayList<PVector> greenPoints = new ArrayList();
ArrayList<PVector> bluePoints = new ArrayList();

void setup() {
  int width = 640;
  int height = 480;
  size(640, 480);
  frameRate(25);
  smooth();
  String[] cameras = Capture.list();

  if (cameras.length == 0) {
    println("There are no cameras available for capture.");
    exit();
  } else {
    println("Available cameras:");
    for (int i = 0; i < cameras.length; i++) {
      println(cameras[i]);
    }
    video = new Capture(this, width, height);
    video.start();     
  }      
}

void captureEvent(Capture video) {
  video.read();
}

void draw() {
  background(255);
  video.loadPixels();
  image(video, 0 , 0);  

  findRed();
  findGreen();
  findBlue();
}

void findRed(){
  trackRed = color(255, 0, 0);

  float worldRecord = 500; 

  int closestRedX = 0;
  int closestRedY = 0;

  for (int x = 0; x < video.width; x ++ ) {
    for (int y = 0; y < video.height; y ++ ) {
      int loc = x + y*video.width;

      // What is current color
      color currentColor = video.pixels[loc];

      float r1 = red(currentColor);
      float g1 = green(currentColor);
      float b1 = blue(currentColor);
      float r2 = red(trackRed);
      float g2 = green(trackRed);
      float b2 = blue(trackRed);

      // Using euclidean distance to compare colors
      float d = dist(r1, g1, b1, r2, g2, b2);



      // If current color is more similar to tracked color than
      // closest color, save current location and current difference
      if (d < worldRecord) {
        worldRecord = d;
        closestRedX = x;
        closestRedY = y;
      }
    }
  }

  // We only consider the color found if its color distance is less than 10. 
  // This threshold of 10 is arbitrary and you can adjust this number depending on how accurate you require the tracking to be.
  if (worldRecord < threshold) { 

    // Draw a circle at the tracked pixel
    fill(trackRed);
    strokeWeight(4.0);
    ellipse(closestRedX, closestRedY, 16, 16);
    redPoints.add(new PVector(closestRedX, closestRedY));
  }

  // Limit it to the last 1000 points.
  while( redPoints.size() > 1000 ){
    redPoints.remove(0);
  }

  // Draw a line between all the points.
  for(int i = 0; i < redPoints.size()-1; i++){
    stroke(trackRed);
    line(redPoints.get(i).x,redPoints.get(i).y,redPoints.get(i+1).x,redPoints.get(i+1).y);
  }
}

void findGreen(){
 trackGreen = color(0, 255, 0);
  float worldRecord = 500; 
  int closestGreenX = 0;
  int closestGreenY = 0;

  for (int x = 0; x < video.width; x ++ ) {
    for (int y = 0; y < video.height; y ++ ) {
      int loc = x + y*video.width;
      color currentColor = video.pixels[loc];
      float r1 = red(currentColor);
      float g1 = green(currentColor);
      float b1 = blue(currentColor);
      float r2 = red(trackGreen);
      float g2 = green(trackGreen);
      float b2 = blue(trackGreen);

      float d = dist(r1, g1, b1, r2, g2, b2);
      if (d < worldRecord) {
        worldRecord = d;
        closestGreenX = x;
        closestGreenY = y;
      }
    }
  }

  if (worldRecord < threshold) { 
    fill(trackGreen);
    strokeWeight(4.0);
    ellipse(closestGreenX, closestGreenY, 16, 16);
    greenPoints.add(new PVector(closestGreenX, closestGreenY));
  }

  while( greenPoints.size() > 1000 ){
    greenPoints.remove(0);
  }

  for(int i = 0; i < greenPoints.size()-1; i++){
    stroke(trackGreen);
    line(greenPoints.get(i).x,greenPoints.get(i).y,greenPoints.get(i+1).x,greenPoints.get(i+1).y);
  }
}

void findBlue(){
  trackBlue = color(0, 0, 255);
  float worldRecord = 500; 
  int closestBlueX = 0;
  int closestBlueY = 0;

  for (int x = 0; x < video.width; x ++ ) {
    for (int y = 0; y < video.height; y ++ ) {
      int loc = x + y*video.width;
      color currentColor = video.pixels[loc];
      float r1 = red(currentColor);
      float g1 = green(currentColor);
      float b1 = blue(currentColor);
      float r2 = red(trackBlue);
      float g2 = green(trackBlue);
      float b2 = blue(trackBlue);

      float d = dist(r1, g1, b1, r2, g2, b2);
      if (d < worldRecord) {
        worldRecord = d;
        closestBlueX = x;
        closestBlueY = y;
      }
    }
  }

  if (worldRecord < threshold) { 
    fill(trackBlue);
    strokeWeight(4.0);
    ellipse(closestBlueX, closestBlueY, 16, 16);
    bluePoints.add(new PVector(closestBlueX, closestBlueY));
  }

  while( bluePoints.size() > 1000 ){
    bluePoints.remove(0);
  }

  for(int i = 0; i < bluePoints.size()-1; i++){
    stroke(trackBlue);
    line(bluePoints.get(i).x,bluePoints.get(i).y,bluePoints.get(i+1).x,bluePoints.get(i+1).y);
  }
}

void keyPressed() {
  if (key == ENTER) {
    // clear screen / undo

    if (redPoints.size() > 0){
      for (int i = 0; i < redPoints.size(); i++) {
        redPoints.remove(i);
      } 
    }

    if (greenPoints.size() > 0){
      for (int i = 0; i < greenPoints.size(); i++) {
        greenPoints.remove(i);
      } 
    }

    if (bluePoints.size() > 0){
      for (int i = 0; i < bluePoints.size(); i++) {
        bluePoints.remove(i);
      } 
    }
  }
}
```
