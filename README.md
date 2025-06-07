# 🚗 ESP32 GPS Speedometer
### Created by **Michael Hogue**

An advanced, battery-powered **portable GPS speedometer** built with an ESP32 DevKit v4, rotary encoder UI, and 20×4 I²C LCD. Includes real-time speed, direction, trip tracking, deep sleep support, and EEPROM trip persistence.

---

## 📦 Features

- 🛰️ Live GPS Speed (in MPH)
- 🧭 Direction (cardinal + degrees)
- 📍 Distance tracking (in miles)
- ⏱️ Total trip time with pause/resume
- 🔋 Battery voltage + percentage
- 🔄 Max speed and average speed
- 🌀 Rotary encoder for screen navigation
- 🔘 Encoder button for reset / deep sleep
- 🌙 Auto deep sleep after inactivity (3 minutes)
- 🧠 EEPROM (NVS) trip data persistence
- 🔧 Config screen with backlight toggle
- 👋 Splash screen on startup

---

## 🔧 Hardware Used

| Module              | Description                            |
|---------------------|----------------------------------------|
| ESP32 DevKit v4     | Main microcontroller (WROOM-32D/U)     |
| GPS Module          | NEO-6M or similar                      |
| LCD (I2C 20×4)      | PCF8574 backpack (I2C address 0x27)    |
| Rotary Encoder      | EC11 with switch                       |
| Battery Divider     | 1:1 voltage divider (100kΩ:100kΩ)      |
| Power Source        | 3.7V Li-ion battery or USB             |

---

## 🧠 Pinout (ESP32 DevKit v4)

| Function            | ESP32 GPIO | Notes                            |
|---------------------|------------|----------------------------------|
| I2C SDA (LCD)       | GPIO21     | PCF8574 LCD interface            |
| I2C SCL (LCD)       | GPIO22     |                                  |
| GPS RX (from GPS)   | GPIO16     | Connect to GPS TX                |
| GPS TX              | GPIO17     | Not used                         |
| Battery Voltage     | GPIO36     | ADC1_CH0                         |
| Encoder CLK (A)     | GPIO33     | Rotary signal                    |
| Encoder DT (B)      | GPIO25     | Rotary signal                    |
| Encoder SW (button) | GPIO26     | With `INPUT_PULLUP`              |

> **Power**: Use 3.3V for GPS, LCD, and Encoder. Do NOT apply 5V directly to ESP32 GPIOs.
---
⚡ Battery Voltage Divider Calculator
To safely measure higher voltages (like 4.2V–5.0V) with the ESP32 ADC (max 3.3V), use a resistive divider:

css
Copy
Edit
BAT+ ── R1 ─┬───> GPIO36 (ADC input)
            │
           R2
            │
           GND
🧮 Voltage at ADC = Vbattery × R2 / (R1 + R2)

Recommended Values:
Vbattery Max	R1	R2	Divider Ratio	ADC Voltage
4.2V	100k	100k	0.5	2.1V
5.0V	150k	100k	0.4	2.0V

🔒 Keep ADC input under 3.3V to avoid damage.
---

## 📺 Screens

1. **Speed + Direction**  
2. **Distance + Time**  
3. **GPS Sat Count + Fix Age**  
4. **Trip Stats (Max / Avg speed)**  
5. **Config (Backlight, Reset)**  
6. **Shutdown (manual sleep)**

Use **rotary encoder** to switch screens.  
Hold button on:
- **Config** screen → Reset trip
- **Shutdown** screen → Deep sleep

---

## ⏲ Sleep Behavior

- 💤 Auto sleep after **3 minutes** of no movement
- 📥 Trip data is saved to **NVS EEPROM**
- 🌄 On wake, trip continues from last point

---

## 🔧 Software Setup

### ✅ Arduino IDE Requirements:
- **Board**: ESP32 Dev Module
- **Libraries**:
  - `TinyGPSPlus`
  - `LiquidCrystal_I2C`
  - `Preferences`

### ⚙ Upload Settings:
- CPU Freq: 240 MHz
- Flash Mode: QIO or DIO
- Partition: Default (4MB)

---

## 🧰 TODO / Ideas

- [ ] Add microSD for trip logging
- [ ] Add BLE to sync data
- [ ] Add IMU for motion filtering
- [ ] External reset or power switch

---

## 📜 License

MIT License © 2025 Michael Hogue  
You are free to use, modify, and distribute this project with attribution.

---
