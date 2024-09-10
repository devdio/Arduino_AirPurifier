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
  
### 온습도 센서

```c
#include <DHT11.h>

#define DHTPIN 4
DHT11 dht11(DHTPIN);

void setup() {
    Serial.begin(9600);
}

void loop() {
    int temperature = 0;
    int humidity = 0;

    int result = dht11.readTemperatureHumidity(temperature, humidity);

    if (result == 0) {
        Serial.print("Temperature: ");
        Serial.print(temperature);
        Serial.print(" °C\tHumidity: ");
        Serial.print(humidity);
        Serial.println(" %");
    } else {
        Serial.println(DHT11::getErrorString(result));
    }
}
```

### 릴레이(FAN) 동작
```c
int FAN = 3 ;

void setup() {
  pinMode(FAN,OUTPUT);

}

void loop() {
 digitalWrite(FAN, HIGH);
 delay(5000);
 digitalWrite(FAN, LOW);
 delay(5000);
}
```

### 먼지 센서

```c
//Dust라는 변수 선언과 미세먼지 값, 습도 값, 온도 값 문자열을 담기위한 배열 선언
int Dust = 0;

//각 핀과 연결된 핀 번호를 저장할 변수 선언 
int Vo = A0 ;
int V_LED = 2 ;

//미세먼지값 측정을 위한 데이터값 변수 선언
float Vo_value = 0;
float Voltage = 0;

void setup()
{     
  // 시리얼 통신 시작
  Serial.begin(9600);

  //핀모드 입출력 설정
  pinMode(V_LED, OUTPUT);
  pinMode(Vo, INPUT);
}

void loop()
{
  // 시리얼 모니터 출력
  Serial.println("ok");
  
  //LOW를 줘서 내부의 적외선을 켠다.
  digitalWrite(V_LED, LOW);
  delayMicroseconds(280);
  Vo_value = analogRead(Vo);
  delayMicroseconds(40);
  digitalWrite(V_LED,HIGH);
  delayMicroseconds(9680);
  
  /*
  전압[V] = (아날로그 핀 값) * 5.0 / 1024
  미세먼지 센서의 출력전압(Vo)는 먼지가 없을 때의 출력전압(Voc)과 미세먼지 농도에 비례하여 출력 
  */
 
  Voltage = Vo_value * 5.0 / 1024.0;
  Serial.println(Voltage);
  
  if( Voltage < 0.6 ){
    Dust = 0;
  }
  else {
    // 이 수식은 먼지 센서에서 측정된 전압 신호를 실제 먼지 농도로 변환합니다. 
    // 센서의 출력 전압은 공기 중의 먼지 농도에 따라 달라지며, 이 수식을 통해 그 농도를 계산할 수 있습니다.
    Dust = 172*Voltage - 103.2;
  }
  Serial.println(Dust);
  delay(500);
}
```

















