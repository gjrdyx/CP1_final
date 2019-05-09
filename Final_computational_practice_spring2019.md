# Light Hidden Houses
This is an Arduino project that simulates a type of building hides from light.

## Summary

The project makes a sense of how an area of buildings move down under the ground, so that they are able to hide from light and heat.
It will react to the environment, basic on the light condition. When the light is too much, all the buildings will hide underground, 
while if light is suitable for people activites, they will go up. If it is so dark, such as night, the lights in the buildings will on.

## Component Parts

-Arduino Uno board
-LEDs
-Wires
-Photoresistor
-Servos
-USB Cable
-Breadboard
-200 resistor
-10K resistor

## Timeline

What did you do in each of the past four weeks?

- Week 0: Write Proposal
- Week 1: Work on code that makes servo and photoresistor work together.
- Week 2: Make different units with LED, set servo on the base and connect them to Arduino Uno board.
- Week 3: Make the main body with LEGO and set everthing on the base.
- Week 4: Present!

## Challenges

The hard part was to think about how to transfer rotation to vertical movement and the structure that allows the six units 
are able to be moved by only two servos. And after deciding add LEDs in each units, leaving space to let wiresgo through took
me a long time. Also, learning and trying to combine all the components work together is really excieted.

## Complete Work

Code
```
#include <Servo.h>
Servo myservo;
int ldrPin = A0;
int pos = 0;
bool raised = false;
int bottom = 50;
int top = 140;
int LED = 13;

void setup() {
  myservo.attach(9);
  myservo.write(bottom);
  Serial.begin(9600);
  Serial.println("Startup");
  pinMode(LED, OUTPUT);
}

void loop() {
  int ldrStatus = analogRead(ldrPin);
  Serial.println(ldrStatus);

  if (ldrStatus < 160 && raised) {
    Serial.println("lowering");
    raised = false;
    for (int i = top; i > bottom; i--) {
      myservo.write(i);
      delay(10);
    }
  }

  if (ldrStatus > 200 && !raised) {
    Serial.println("raising");
    raised = true;
    for (int i = bottom; i < top; i++) {
      myservo.write(i);
      delay(10);
    }  
    }
     if (ldrStatus > 320) {
      digitalWrite(LED,HIGH);  
    }
    if (ldrStatus < 320) {
      digitalWrite(LED,LOW);  
    }
}
```
Arduino pieces
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/Aruino.JPG)
Base & Servo
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/BaseServo.JPG)
Main Body Ground
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/MainBody_Ground.JPG)
Main Body Units & Structure
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/MainBody_Units.jpg)
Dark environment
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/CompleteWork_Dark.JPG)
Medium light environment
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/CompleteWork_MediumLight.JPG)
Strong light environment
![alt text](https://github.com/gjrdyx/CP1_final/blob/master/CompleteWork_StrongLight.JPG)
