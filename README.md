# Introduction

The IoT-Based Smart Egg Incubator is designed to maintain the optimal temperature and humidity for incubating eggs.
It uses a DHT11 sensor to measure temperature and humidity, an ESP32 to process the data and control the relay and fan, 
and Blynk to monitor and control the incubator remotely.

# Components
- ESP32
- DHT11 sensor
- 12V DC fan
- Relay module 2 NOs
- LiquidCrystal_I2C (LCD 16x2)
- Connecting wires
- Breadboard
- Power supply
- Incandescent bulb

# Circuit Diagram
![WhatsApp Image 2024-07-12 at 00 32 53](https://github.com/user-attachments/assets/5daa0f09-8b57-4b34-807a-41da7f3a0e37)


# Installation

  **1.Hardware Setup:**
  - Connect the DHT11 sensor to the ESP32 (DHTPIN to GPIO 26).
  - Connect the relay module to the ESP32 (RELAY_PIN to GPIO 2).
  - Connect the 12V DC fan to the ESP32 (FAN_PIN to GPIO 4).
  - Connect the LCD to the ESP32 using I2C.

  **Software Setup:**

  - Download and install the Arduino IDE from Arduino website.
  - Install the following libraries in Arduino IDE:
    - Blynk
    - LiquidCrystal_I2C
    - DHT sensor library
  - Connect the ESP32 to your computer and upload the provided code.

# Usage

  **1.Connecting to Wi-Fi:**
  
  - Update the Wi-Fi credentials in the code:
    
      ```php
      char ssid[] = "Your_SSID";
      char pass[] = "Your_PASSWORD";
      ```
   **2.Blynk Setup:**

   - Download the Blynk app from the Google Play Store or Apple App Store.
   - Create a new project and add the following widgets:
     - Value Display (V1) for Temperature
     - Value Display (V2) for Humidity
     - LED (V3) for Relay Status
     - LED (V4) for Fan Status
   - Copy the Blynk Auth Token and update it in the code

     ```php
        #define BLYNK_AUTH_TOKEN "Your_Auth_Token"
     ```
     **3.Running the System:**
     
     - Power on the ESP32.
     - Monitor the temperature and humidity on the LCD and the Blynk app.
     - The relay and fan will be controlled automatically based on the temperature readings.

# Key Functions

   - **setup()** Initializes serial communication, Blynk, LCD, DHT sensor, and sets pin modes for the relay and fan.
   - **loop()** Continuously reads temperature and humidity, updates the LCD and Blynk app, and controls the relay and fan based on the temperature.
   - **sendSensorData()** Sends sensor data to the Blynk app every second.

# Bynk Output 

![WhatsApp Image 2024-05-14 at 21 19 13 (1)](https://github.com/user-attachments/assets/6cb4a727-6dfd-4f94-9816-caeb65b0916c)



 
    
     
   
