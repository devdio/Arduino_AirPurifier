# 공기청정기 코드
  
### LED 출력

- RED만 깜빡이기 
```c
int R_LED = 5 ;
int Y_LED = 6 ;
int G_LED = 7 ;

void setup()
{     
  //핀모드 입출력 설정
  pinMode(R_LED, OUTPUT);
  pinMode(Y_LED, OUTPUT);
  pinMode(G_LED, OUTPUT);
}

void loop()
{
  digitalWrite(R_LED, HIGH);
  delay(500);
  digitalWrite(R_LED, LOW);
  delay(500);
}
```

- 신호등 깜빡이기  
```c
int R_LED = 5 ;
int Y_LED = 6 ;
int G_LED = 7 ;

void setup()
{     
  //핀모드 입출력 설정
  pinMode(R_LED, OUTPUT);
  pinMode(Y_LED, OUTPUT);
  pinMode(G_LED, OUTPUT);
}

void loop()
{
  digitalWrite(R_LED, HIGH);
  delay(500);
  digitalWrite(R_LED, LOW);
  delay(500);
  digitalWrite(Y_LED, HIGH);
  delay(500);
  digitalWrite(Y_LED, LOW);
  delay(500);
  digitalWrite(G_LED, HIGH);
  delay(500);
  digitalWrite(G_LED, LOW);
  delay(500); 
}
```
