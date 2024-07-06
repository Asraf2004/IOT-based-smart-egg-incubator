#define BLYNK_TEMPLATE_ID "TMPL3FPtuykcM"
#define BLYNK_TEMPLATE_NAME "smart egg"
#define BLYNK_AUTH_TOKEN "aLUZbdsbPiLa0jsu_UHvkMWyDKNqdT8W"

#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>
#include <BlynkSimpleEsp32.h>

#define DHTPIN 26      // Digital pin connected to the DHT sensor
#define DHTTYPE DHT11  // DHT 11

#define RELAY_PIN 2    // Digital pin connected to the relay
#define FAN_PIN 4      // Digital pin connected to the fan

char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = "AsrafAhamed";     // Your WiFi SSID
char pass[] = "88888888";

DHT dht(DHTPIN, DHTTYPE);

LiquidCrystal_I2C lcd(0x27, 16, 2);  // Set the LCD address to 0x27 for a 16 chars and 2 line display

BlynkTimer timer;

void setup() {
  Serial.begin(9600);
  Blynk.begin(auth, ssid, pass);
  lcd.init();                      // Initialize LCD
  lcd.backlight();                 // Turn on backlight
  dht.begin();
  pinMode(RELAY_PIN, OUTPUT);
  pinMode(FAN_PIN, OUTPUT);
  
  // Turn on relay by default
  digitalWrite(RELAY_PIN, LOW); // Assuming LOW state turns the relay ON
  digitalWrite(FAN_PIN, HIGH); // Assuming HIGH state turns the relay OFF
  
  // Setup a function to be called every second
  timer.setInterval(1000L, sendSensorData);
}

void loop() {
    // Wait for 2 seconds between measurements
  
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();

  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  if (temperature >= 30.0) {
    Blynk.logEvent("temperature_alert", "Temperature exceeded 40 degrees Celsius!");
  }

  lcd.setCursor(0, 0);
  lcd.print("Humidity: ");
  lcd.print(humidity);
  lcd.print("%");

  lcd.setCursor(0, 1);
  lcd.print("Temp: ");
  lcd.print(temperature);
  lcd.print("C");

  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print("%Temperature: ");
  Serial.print(temperature);
  Serial.println("C");

  if (temperature >= 38.0) {
    digitalWrite(RELAY_PIN, HIGH); // Turn off relay
  } else if (temperature <= 37.0) {
    digitalWrite(RELAY_PIN, LOW); // Turn on relay
  }

  // Control the fan based on temperature
  if (temperature >= 38.0) {
    digitalWrite(FAN_PIN, LOW); // Turn on fan
  } else if (temperature <= 37.0) {
    digitalWrite(FAN_PIN, HIGH); // Turn off fan
  }
  
  Blynk.run();
  timer.run();
}

void sendSensorData() {
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();

  if (isnan(temperature) || isnan(humidity)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  // Send temperature and humidity data to Blynk app
  Blynk.virtualWrite(V1, temperature);
  Blynk.virtualWrite(V2, humidity);

  Blynk.virtualWrite(V3, digitalRead(RELAY_PIN));
  Blynk.virtualWrite(V4, digitalRead(FAN_PIN));

  Blynk.virtualWrite(V5, temperature);
}

  
