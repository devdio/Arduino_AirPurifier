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

### Text LED
- 기본 출력
```c
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <Emotion_Farm.h>
 
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(9600);

  lcd.init();
  lcd.backlight();
  lcd.home();
  delay(500);

  lcd.setCursor(2,0);
  lcd.print("SMART");
  delay(1000);
  lcd.setCursor(8,0);
  lcd.print("GARDEN");
  delay(1000);
  lcd.clear();
}

void loop() {

}
```

-  아이콘 표시
```c
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <Emotion_Farm.h>
 
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  Serial.begin(9600);

  //LCD에 인트로 출력
  lcd.init();
  lcd.backlight();
  lcd.home();
  delay(500);

  // 부팅시 LCD에 메세지 표시  
  lcd.setCursor(2,0);
  lcd.print("SMART");
  delay(1000);
  lcd.setCursor(8,0);
  lcd.print("GARDEN");
  delay(1000);
  lcd.clear();

  // 라이브러리로 추가한 특수 문자 및 이모티콘 추가
  lcd.createChar(0, temp);
  lcd.createChar(1, C);
  lcd.createChar(2, humi);  
  lcd.createChar(3, Qmark);
  lcd.createChar(4, water);
  lcd.createChar(5, good);
  lcd.createChar(6, wind);
}

void loop() {
  for(int i=0; i<7; i++) {
    lcd.setCursor(i, 0);
    lcd.write(i);
    delay(500);
  }

  // 0.5초마다 측정한다.
  delay(500);
}
```
