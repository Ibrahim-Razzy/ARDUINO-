#include<LiquidCrystal.h>

LiquidCrystal lcd(12 , 11 , 5 ,4 ,3 ,2);
int sensorPin=A0;
int redLed = 7;
int greenLed = 8;
const int buzzer=13;
int sensorThres=900;
int analoguesensor;
void setup()
 {
Serial.begin(9600);
pinMode(sensorPin , INPUT);
pinMode(redLed, OUTPUT);
pinMode(greenLed, OUTPUT);
  
}

void loop() {
  analoguesensor = analogRead(sensorPin);
   lcd.setCursor (0,1);
  lcd.print( analoguesensor);
  //lcd.setCursor (1,2);
 // delay (3000);
Serial.print("A 0");
Serial.println(analoguesensor);
  if(analoguesensor>sensorThres)//(digitalRead(Gas) == HIGH)
  {
    lcd.setCursor(0,1);
    lcd.print("SMOKE DETECTED");
  //delay(5000);
    digitalWrite(7, HIGH);
    digitalWrite(8, LOW);
    tone(buzzer, 1500, 200);
    delay(500);
    //tone(buzzer, 1000, 200);
  }
else
{
  lcd.setCursor(0,1);
  lcd.print(" NORMAL LEVEL ");
  //delay(5000);
  digitalWrite(8, HIGH);
  digitalWrite(7 ,LOW);
  noTone(buzzer);
}
delay(100);
lcd.clear();
}
