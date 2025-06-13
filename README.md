# 코드

#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

byte m = 0;
byte s = 0;
byte ps = 0;
boolean sw;
byte stat = 0;

void setup() {
  lcd.begin(16, 2);
  lcd.setCursor(3, 0);
  lcd.print("STOP WATCH");
  lcd.setCursor(4, 1);
  lcd.print("0 /0 /0 ");
  pinMode(7, INPUT_PULLUP);
}

void counter() {
  delay(100);
  ps++;
  if (ps == 10) {
    ps = 0;
    s++;
    if (s == 60) {
      s = 0;
      m++;
      lcd.setCursor(8, 1);
      lcd.print(" ");
    }
  }

  lcd.setCursor(10, 1);
  lcd.print(ps);
  lcd.setCursor(7, 1);
  lcd.print(s);
  lcd.setCursor(4, 1);
  lcd.print(m);
}

void loop() {
  sw = digitalRead(7);
  if (sw == 0) {
    while (sw == 0) {
      sw = digitalRead(7);
    }
    stat++;
  }

  switch (stat) {
    case 1:
      counter();
      break;
    case 2:
      break;
    case 3:
      ps = 0;
      s = 0;
      m = 0;
      lcd.setCursor(4, 1);
      lcd.print("0 /0 /0 ");
      stat = 0;
      break;
  }
}

