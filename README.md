# arduino
```arduino
int a= 9;
int b=10;
void setup() {
  pinMode(5,INPUT_PULLUP);
  pinMode(a, OUTPUT);
  pinMode(b, OUTPUT);
}

void loop() {
  int value;
  value=digitalRead(5);
  if(value==0)   //如果是0的話就會亮
  {
  digitalWrite(a,1 );
  digitalWrite(b,0);   
  }
  else
  {           
  digitalWrite(a, 0);    
  digitalWrite(b,1);
  }                     
}
```
