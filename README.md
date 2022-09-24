arduino
按鈕開燈
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