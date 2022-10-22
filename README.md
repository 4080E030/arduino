# arduino
## 按鈕開燈
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
  digitalWrite(a,1 );  // a亮,b不會亮 ，要亮兩個就都改1
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



const int buttonPin = 5;    
const int ledPin1 = 9;
const int ledPin2 = 10; 
//const int ledPin = 13; 

int ledState = HIGH;         
int buttonState;             
int lastButtonState = LOW;  


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

  

 
  if (reading != lastButtonState) {
    
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
```
