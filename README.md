# Wi-Fi Face Buddy
Wi-Fi Face Buddy is a fun and expressive IoT desk companion built using ESP32. It displays a blinking face, senses temperature using DHT11, shows Wi-Fi stats when touched, and controls a relay wirelessly using another ESP32.

---

## Features
- OLED screen with a blinking animated face
- Touch sensor to trigger Wi-Fi and temperature display
- RGB LED with cycling colors
- Sends HTTP request to another ESP32 to control a relay when temp > 30°C
- Works entirely over local Wi-Fi (no cloud)

---

## Components Used

- ESP32 x2
- SSD1306 OLED Display (I2C)
- DHT11 Temperature Sensor
- RGB LED (Common Cathode)
- TTP223 Touch Sensor
- Relay Module
- Jumper wires, breadboard

---

## Wiring (Main ESP32)
| Component     | ESP32 Pin  |
|---------------|------------|
| OLED SDA      | GPIO 21    |
| OLED SCL      | GPIO 22    |
| RGB Red       | GPIO 25    |
| RGB Green     | GPIO 26    |
| RGB Blue      | GPIO 27    |
| Touch OUT     | GPIO 4     |
| DHT11 Data    | GPIO 5     |

---

## Wiring (Relay ESP32)
| Component   | ESP32 Pin |
|-------------|-----------|
| Relay IN    | GPIO 23   |

---

## Code Structure
- `esp32_main/main_device.ino`: The main logic including display, sensors, Wi-Fi, and HTTP requests.
- `esp32_relay/relay_device.ino`: Minimal HTTP server to trigger relay ON/OFF via GET request.

---

## How It Works
1. Main ESP32 boots, connects to Wi-Fi, and shows a blinking face.
2. On touch, it displays:
   - IP address
   - RSSI (Wi-Fi signal strength)
   - Temperature from DHT11
3. If temperature > 30°C, it sends an HTTP GET request to the second ESP32.
4. The second ESP32 listens for `/relay/on` and turns on the relay.
