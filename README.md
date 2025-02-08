# IoT-Smart-Garden---Automatic-watering-system 

This project demonstrates how to read analog voltages from temperature and humidity sensors using the STM32F103C8T6 microcontroller. 
The data was then transmitted via the UART protocol to the ESP32, displayed on an LCD screen, and used to control a water pump for plant irrigation. 
Subsequently, the ESP32 transmitted the data to a web server
## Project Overview

In this project:
- The **STM32** collects data (e.g., sensor readings, status information, etc.).
- The **ESP32** acts as a Wi-Fi gateway, receiving data from the STM32 via UART.
- The **ESP32** sends the data over a **TCP/IP** connection to a server or another device on the network.

The following diagram illustrates the system architecture:

![System Overview](https://github.com/quynhphamduong/IoT-Smart-Garden---Automatic-watering-system/blob/9525ff16d472fe18a5743a2d322e12d83687c895/Block%20diagram.png)  
*Insert an image showing the architecture of your system: STM32 → ESP32 → TCP/IP Network*

## Features

- **STM32** microcontroller for data acquisition.
- **ESP32** as a Wi-Fi gateway to transmit data via TCP/IP.
- Communication between STM32 and ESP32 using UART (Serial).
- Data sent over TCP/IP to a server or another network device.

## Installation & Setup

### 1. Hardware Requirements
- **STM32** development board (e.g., STM32F4, STM32F1).
- **ESP32** development board (e.g., ESP32 DevKit V1).
- Jumper wires for UART communication between STM32 and ESP32.
- Power supply for both STM32 and ESP32 boards.

### 2. Software Requirements
- **STM32 IDE** (e.g., STM32CubeIDE or KEIL).
- **ESP32 Toolchain** (e.g., Arduino IDE or ESP-IDF).
- **TCP/IP Server** to receive data from the ESP32.

### 3. Wiring Connections
- **STM32 TX → ESP32 RX**
- **STM32 RX → ESP32 TX**
- **GND → GND**

### 4. Firmware for STM32
- Clone this repository or download the source code for the STM32 firmware.
- Open the project in **STM32CubeIDE** or your preferred STM32 IDE.
- Write the necessary code to read data from sensors or input devices and send the data to the ESP32 over UART.

### 5. Firmware for ESP32
- Open the **Arduino IDE** (or ESP-IDF if you're using that).
- Install the ESP32 board support via the Arduino Board Manager.
- Flash the ESP32 with the firmware that reads data from the STM32 over UART and sends it over TCP/IP.
  Example ESP32 code (Arduino IDE):
  ```cpp
  #include <WiFi.h>

  const char* ssid = "your_wifi_ssid";
  const char* password = "your_wifi_password";
  const char* host = "server_ip_address";
  const int port = 12345;  // Server port

  void setup() {
    Serial.begin(115200);  // UART baud rate to match STM32

    // Connect to Wi-Fi
    WiFi.begin(ssid, password);
    while (WiFi.status() != WL_CONNECTED) {
      delay(1000);
      Serial.println("Connecting to WiFi...");
    }
    Serial.println("Connected to WiFi!");

    // Connect to the server
    WiFiClient client;
    if (!client.connect(host, port)) {
      Serial.println("Connection to server failed.");
      return;
    }
    Serial.println("Connected to server.");
  }

  void loop() {
    if (Serial.available() > 0) {
      String data = Serial.readString();
      client.println(data);  // Send data to server
    }
    delay(100);
  }
# Automatic-watering-system

[def]: .png
