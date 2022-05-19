# ino
Archivos de Arduino 

En este `README.md` incluir todas las especificaciones de placa e incorporar la esquemática con imagen y/o link a TinkerCad.

=programacion stepper=


/*
 * Simple demo, should work with any driver board
 *
 * Connect STEP, DIR as indicated
 *
 * Copyright (C)2015-2017 Laurentiu Badea
 *
 * This file may be redistributed under the terms of the MIT license.
 * A copy of this license has been included with this distribution in the file LICENSE.
 */
#include <Arduino.h>
#include "BasicStepperDriver.h"

// Motor steps per revolution. Most steppers are 200 steps or 1.8 degrees/step
#define MOTOR_STEPS 200
#define RPM 20

// Since microstepping is set externally, make sure this matches the selected mode
// If it doesn't, the motor will move at a different RPM than chosen
// 1=full step, 2=half step etc.
#define MICROSTEPS 1

// All the wires needed for full functionality
#define DIR 4
#define STEP 5
//Uncomment line to use enable/disable functionality
#define SLEEP 6 //13

// 2-wire basic config, microstepping is hardwired on the driver
BasicStepperDriver stepper(MOTOR_STEPS, DIR, STEP);

//Uncomment line to use enable/disable functionality
//BasicStepperDriver stepper(MOTOR_STEPS, DIR, STEP, SLEEP);

int analogPin = A3; // potentiometer wiper (middle terminal) connected to analog pin 3
                    // outside leads to ground and +5V
int val = 0;  // variable to store the value read

void setup() {

pinMode(2, OUTPUT);
digitalWrite(2, LOW);
  //digitalWrite(ENABLE, HIGH);
    stepper.begin(RPM, MICROSTEPS);
    
    // if using enable/disable on ENABLE pin (active LOW) instead of SLEEP uncomment next line
    stepper.setEnableActiveState(LOW);
    Serial.begin(9600);           //  setup serial
}

void loop() {
  val = analogRead(analogPin);  // read the input pin
  Serial.println(val);          // debug value
  if( (val < 1000) )
{
   digitalWrite(2, HIGH);
   stepper.rotate(360);

    

    // energize coils - the motor will hold position
    // stepper.enable();
  
    /*
     * Moving motor one full revolution using the degree notation
     */
    
}
 if( (val > 1000) )
{
digitalWrite(2, LOW);
stepper.rotate(0);

}
/*
else {
   while ( (val > 650) && (val < 905))
{
 int site_ = map(val, 630, 940, 1, 200);
  stepper.move (site_);
  val = analogRead(analogPin);
  Serial.println(val);
}
*/
}




  ##Programación leds## 
  
  
  #include <Adafruit_NeoPixel.h>
#include <EEPROM.h>

#define NUM_LEDS 240 
#define PIN 5 
Adafruit_NeoPixel strip = Adafruit_NeoPixel(NUM_LEDS, PIN, NEO_GRB + NEO_KHZ800);

#define BUTTON 2
byte selectedEffect=0;

void setup()
{
  strip.begin();
  strip.show(); // Initialize all pixels to 'off'
  pinMode(2,INPUT_PULLUP);  // internal pull-up resistor
  attachInterrupt (digitalPinToInterrupt (BUTTON), changeEffect, HIGH); // pressed
}

// *** REPLACE FROM HERE ***
void loop() { 
  EEPROM.get(0,selectedEffect); 
  
  if(selectedEffect>1) { 
    selectedEffect=0;
    EEPROM.put(0,0); 
  } 
  
  switch(selectedEffect) {
    
    /*case 0  : {
                // RGBLoop - no parameters
                RGBLoop();
                break;
              }

    case 1  : {
                // FadeInOut - Color (red, green. blue)
                FadeInOut(0xff, 0x00, 0x00); // red
                FadeInOut(0xff, 0xff, 0xff); // white 
                FadeInOut(0x00, 0x00, 0xff); // blue
                break;
              }
              
    case 2  : {
                // Strobe - Color (red, green, blue), number of flashes, flash speed, end pause
                Strobe(0xff, 0xff, 0xff, 10, 50, 1000);
                break;
              }

    case 3  : {
                // HalloweenEyes - Color (red, green, blue), Size of eye, space between eyes, fade (true/false), steps, fade delay, end pause
                HalloweenEyes(0xff, 0x00, 0x00, 
                              1, 4, 
                              true, random(5,50), random(50,150), 
                              random(1000, 10000));
                HalloweenEyes(0xff, 0x00, 0x00, 
                              1, 4, 
                              true, random(5,50), random(50,150), 
                              random(1000, 10000));
                break;
              }
              
    case 4  : {
                // CylonBounce - Color (red, green, blue), eye size, speed delay, end pause
                CylonBounce(0xff, 0x00, 0x00, 4, 10, 50);
                break;
              }
              
    case 5  : {
                // NewKITT - Color (red, green, blue), eye size, speed delay, end pause
                NewKITT(0xff, 0x00, 0x00, 8, 10, 50);
                break;
              }
              
    case 6  : {
                // Twinkle - Color (red, green, blue), count, speed delay, only one twinkle (true/false) 
                Twinkle(0xff, 0x00, 0x00, 10, 100, false);
                break;
              }
              
    case 7  : { 
                // TwinkleRandom - twinkle count, speed delay, only one (true/false)
                TwinkleRandom(20, 100, false);
                break;
              }
              
    case 8  : {
                // Sparkle - Color (red, green, blue), speed delay
                Sparkle(0xff, 0xff, 0xff, 0);
                break;
              }
               
    case 9  : {
                // SnowSparkle - Color (red, green, blue), sparkle delay, speed delay
                SnowSparkle(0x10, 0x10, 0x10, 20, random(100,1000));
                break;
              }
              
    case 10 : {
                // Running Lights - Color (red, green, blue), wave dealy
... (660 lines left)
   
   
   
   
   
   
   
