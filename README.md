#arduino
##按鈕開燈
``` arduino 
int a= 9;
int b= 10;
void setup() {
  pinMode(5,INPUT_PULLUP);
  pinMode(a, OUTPUT);
  pinMode(b, OUTPUT);
}

void loop() {
  int value;
  value=digitalRead(5);
  if(value==0)   //如果是0的話就會亮，0就是按下去
  {
  digitalWrite(a,1 );  // a亮,b不會亮 
  digitalWrite(b,0);   
  }
  else
  {           
  digitalWrite(a, 0);    
  digitalWrite(b,1);
  }                     
}
```


## 他按下去會先亮，按下去後會閃爍。

``` arduino 
int a= 9;
int b=10;
void setup() {
  pinMode(5,INPUT_PULLUP);
  pinMode(a, OUTPUT);
  pinMode(b, OUTPUT);
  digitalWrite(a,0);    
  digitalWrite(b,0);
}

void loop() 
{
  int value;
  value=digitalRead(5);
  while(value==1)   //如果是1的話就會亮
  {
    value=digitalRead(5);
  } 

  digitalWrite(a,1);    
  digitalWrite(b,1);
  delay(500);
  digitalWrite(a,0);    
  digitalWrite(b,0);
  delay(500);
  digitalWrite(a,1);    
  digitalWrite(b,1);
  delay(500);
  digitalWrite(a,0);    
  digitalWrite(b,0);
  delay(500);
                    
}
```
/*
  Debounce

  Each time the input pin goes from LOW to HIGH (e.g. because of a push-button
  press), the output pin is toggled from LOW to HIGH or HIGH to LOW. There's a
  minimum delay between toggles to debounce the circuit (i.e. to ignore noise).

  The circuit:
  - LED attached from pin 13 to ground
  - pushbutton attached from pin 2 to +5V
  - 10 kilohm resistor attached from pin 2 to ground

  - Note: On most Arduino boards, there is already an LED on the board connected
    to pin 13, so you don't need any extra components for this example.

  created 21 Nov 2006
  by David A. Mellis
  modified 30 Aug 2011
  by Limor Fried
  modified 28 Dec 2012
  by Mike Walters
  modified 30 Aug 2016
  by Arturo Guadalupi

  This example code is in the public domain.

  http://www.arduino.cc/en/Tutorial/Debounce
*/

// constants won't change. They're used here to set pin numbers:
const int buttonPin = 5;    // the number of the pushbutton pin
const int ledPin1 = 9;
const int ledPin2 = 10; 
//const int ledPin = 13; // the number of the LED pin

// Variables will change:
int ledState = HIGH;         // the current state of the output pin
int buttonState;             // the current reading from the input pin
int lastButtonState = LOW;   // the previous reading from the input pin

// the following variables are unsigned longs because the time, measured in
// milliseconds, will quickly become a bigger number than can be stored in an int.
unsigned long lastDebounceTime = 0;  // the last time the output pin was toggled
unsigned long debounceDelay = 50;    // the debounce time; increase if the output flickers
int count=0;
void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(ledPin1, OUTPUT);
   pinMode(ledPin2, OUTPUT);

  // set initial LED state
  digitalWrite(ledPin1, 1);
  digitalWrite(ledPin2, 1);
}

void loop() {
  // read the state of the switch into a local variable:
  int reading = digitalRead(buttonPin);

  // check to see if you just pressed the button
  // (i.e. the input went from LOW to HIGH), and you've waited long enough
  // since the last press to ignore any noise:

  // If the switch changed, due to noise or pressing:
  if (reading != lastButtonState) {
    // reset the debouncing timer
    lastDebounceTime = millis();
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
  
    if (reading != buttonState) {
      buttonState = reading;

    
      if (buttonState == HIGH) {
        count=count+1;
        if(count>3) count=1;
      }
    }
  }

  switch (count) {
    case 1:
      digitalWrite(ledPin1,1);
      digitalWrite(ledPin2,0);
      break;
    case 2:
      digitalWrite(ledPin1,0);
      digitalWrite(ledPin2,1);
      break;
    default:
      // if nothing else matches, do the default
      // default is optional
    break;
  }

  // set the LED:


  // save the reading. Next time through the loop, it'll be the lastButtonState:
  lastButtonState = reading;
}
