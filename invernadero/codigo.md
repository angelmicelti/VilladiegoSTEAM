#include "ABlocks_Button.h"
#include "DHT.h"
#include <Wire.h>
#include "ABlocks_LiquidCrystal_I2C.h"
#include <MHZ19.h>
#include <SoftwareSerial.h>

// Pin RX Arduino conectado al pin TX del MHZ19
#define RX_PIN 7
// Pin TX Arduino conectado al pin RX del MHZ19
#define TX_PIN 6
// Pin digital 5 para activación del motor
#define MOTOR 5

// Objeto para sensor MHZ19
MHZ19 myMHZ19;
// Serial requerido por el MHZ19
SoftwareSerial mySerial(RX_PIN, TX_PIN);

double pulsador;
double HumDHT11;
double TempDHT11;
double HumTierra1;
double HumTierra2;
double HumTierra3;
double temperatura;
Button button_debounced_0(0,50);

DHT dht2(2,DHT11);
unsigned long task_time_ms=0;

LiquidCrystal_I2C lcd_1(0x27,16,2);

// Contador para temporizar las mediciones
unsigned long timer = 0;

void setup()
{
  pinMode(0, INPUT);
  pinMode(2, INPUT);
  pinMode(A2, INPUT);
  pinMode(A3, INPUT);
  pinMode(A4, INPUT);
  pinMode(5, OUTPUT);
  dht2.begin();
  Serial.begin(9600);
  Serial.flush();
  
  while(Serial.available()>0)Serial.read();

  mySerial.begin(9600);
  myMHZ19.begin(mySerial);
  // Turn auto calibration ON (OFF autoCalibration(false))
  myMHZ19.autoCalibration();

  lcd_1.begin();
  lcd_1.noCursor();
  lcd_1.backlight();
  lcd_1.setCursor(0, 0);
  lcd_1.print(String("  Invernadero"));
  lcd_1.setCursor(0, 1);
  lcd_1.print(String("   Villadiego"));
  delay(2000);
  HumDHT11 = 0;
  TempDHT11 = 0;
  HumTierra1 = 0;
  HumTierra2 = 0;
  HumTierra3 = 0;
  pulsador = 1;
  lcd_1.clear();
}


void loop()
{    
    if (button_debounced_0.pressed()) {
      lcd_1.clear();
      if ((pulsador < 6)) {
        pulsador = (pulsador + 1);
      }
      else {
        pulsador = 1;
      }

    }

    if((millis()-task_time_ms)>=1000){
      task_time_ms=millis();
      
      if ((temperatura>45)) {
        digitalWrite(MOTOR, HIGH);
      }
      else {
        digitalWrite(MOTOR, LOW);  
      }
      
      if ((pulsador == 1)) {
        HumDHT11 = dht2.readHumidity();
        Serial.println(String("Humedad relativa: ")+String(HumDHT11));
        lcd_1.setCursor(0, 0);
        lcd_1.print(String("Humedad relativa"));
        lcd_1.setCursor(4, 1);
        lcd_1.print(HumDHT11);
        lcd_1.setCursor(11, 1);
        lcd_1.print(String("%"));
      }

      if ((pulsador == 2)) {
        TempDHT11 = dht2.readTemperature();
        int8_t tempMHZ19 = myMHZ19.getTemperature();
        temperatura = (TempDHT11+tempMHZ19)/2;
        Serial.println(String("Temperatura: ")+String(temperatura));
        lcd_1.setCursor(0, 0);
        lcd_1.print(String("Temperatura:"));
        lcd_1.setCursor(4, 1);
        lcd_1.print(temperatura);
        lcd_1.setCursor(11, 1);
        lcd_1.print((char)223);
        lcd_1.setCursor(12, 1);
        lcd_1.print(String("C"));
      }

      if ((pulsador == 3)) {
        HumTierra1 = map(analogRead(A2),0,1023,0,100);
        Serial.println(String("Humedad tierra 1: ")+String(HumTierra1));
        lcd_1.setCursor(0, 0);
        lcd_1.print(String("Humedad tierra 1:"));
        lcd_1.setCursor(4, 1);
        lcd_1.print(HumTierra1);
        lcd_1.setCursor(11, 1);
        lcd_1.print(String("%"));
      }

      if ((pulsador == 4)) {
        HumTierra2 = map(analogRead(A3),0,1023,0,100);
        Serial.println(String("Humedad tierra 2: ")+String(HumTierra2));
        lcd_1.setCursor(0, 0);
        lcd_1.print(String("Humedad tierra 2:"));
        lcd_1.setCursor(4, 1);
        lcd_1.print(HumTierra2);
        lcd_1.setCursor(11, 1);
        lcd_1.print(String("%"));
      }

      if ((pulsador == 5)) {
        HumTierra3 = map(analogRead(A4),0,1023,0,100);
        Serial.println(String("Humedad tierra 3: ")+String(HumTierra3));
        lcd_1.setCursor(0, 0);
        lcd_1.print(String("Humedad tierra 3:"));
        lcd_1.setCursor(4, 1);
        lcd_1.print(HumTierra3);
        lcd_1.setCursor(11, 1);
        lcd_1.print(String("%"));
      }

      if ((pulsador == 6)) {
        int nivelCO2 = myMHZ19.getCO2();
        Serial.println(String("CO2 (ppm): ")+String(nivelCO2));
        lcd_1.setCursor(0, 0);
        lcd_1.print(String("CO2 (ppm):"));
        lcd_1.setCursor(4, 1);
        lcd_1.print(nivelCO2);
        lcd_1.setCursor(11, 1);
        lcd_1.print(String("ppm"));
      }
    }

}
