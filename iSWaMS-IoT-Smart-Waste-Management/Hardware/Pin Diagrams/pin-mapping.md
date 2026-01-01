# 📌 Pin Mapping – iSWaMS IoT Smart Waste Management System

This document presents the **pin configuration** for the iSWaMS project, combining
**clear tables** with **visual wiring/block diagrams** for easier understanding
and faster hardware setup.

## 🎨 Color-Coded Pin Legend

To improve readability across diagrams and wiring references, the following
color convention is used consistently in this project:

| Color | Signal Type | Description |
|-----|------------|------------|
| 🔴 Red | Power (VCC) | 3.3V / 5V supply |
| ⚫ Black | Ground (GND) | Common ground |
| 🟡 Yellow | Digital I/O | GPIO signals |
| 🔵 Blue | SPI Lines | SCK, MISO, MOSI |
| 🟢 Green | I2C / UART | SDA, SCL, RX, TX |
| 🟣 Purple | Analog | ADC inputs |
| 🟠 Orange | Control | CS, RST, DIO |

## 🔌 Power-Domain Architecture

The iSWaMS system uses **multiple power domains** to ensure stability and
prevent brownout conditions.

### Power Distribution

- **3.3V Domain**
  - ESP32
  - LoRa (SX1278)
  - RFID (RC522)
  - DHT22
  - Flame Sensor

- **5V Domain**
  - HC-SR04 Ultrasonic Sensor
  - PIR Sensor
  - GPS Module (Neo-6M, powered via onboard regulator)

- **External Supply**
  - Used for GPS and high-current peripherals
  - Grounds are shared with ESP32 (common GND)

⚠️ LoRa and RFID **must NOT** be powered from 5V.

---

## 🔹 1. Transmitter Node (Smart Bin – ESP32)

### 🧠 ESP32 Dev Module

- Logic Level: **3.3V**
- Shared SPI Bus: **LoRa + RFID**
- UART used for **GPS**

---

## 📡 LoRa Module (Ra-02 / SX1278)

### 📊 Pin Mapping Table

| LoRa Pin | ESP32 GPIO | Function |
|--------|------------|---------|
| 🔴 VCC | 🔴 3.3V | Power |
| ⚫ GND | ⚫ GND | Ground |
| 🔵 SCK | 🔵 GPIO 18 | SPI Clock |
| 🔵 MISO | 🔵 GPIO 19 | SPI MISO |
| 🔵 MOSI | 🔵 GPIO 23 | SPI MOSI |
| 🟠 NSS | 🟠 GPIO 32 | Chip Select |
| 🟠 RST | 🟠 GPIO 14 | Reset |
| 🟠 DIO0 | 🟠 GPIO 4 | Interrupt |

---

## 📏 Ultrasonic Sensor (HC-SR04)

### 📊 Pin Mapping Table

| HC-SR04 Pin | ESP32 GPIO | Function |
|-------------|------------|----------|
| 🔴 VCC | 🔴 5V (VIN) | Power |
| ⚫ GND | ⚫ GND | Ground |
| 🟡 TRIG | 🟡 GPIO 25 | Trigger |
| 🟣 ECHO | 🟣 GPIO 34 | Echo (Input only) |

---

## 🌡️ Temperature & Humidity Sensor (DHT22)

### 📊 Pin Mapping Table

| DHT22 Pin | ESP32 GPIO | Function |
|---------|------------|---------|
| 🔴 VCC | 🔴 3.3V | Power |
| 🟡 DATA | 🟡 GPIO 26 | Data |
| ⚫ GND | ⚫ GND | Ground |

---

## 🔥 Flame Sensor

### 📊 Pin Mapping Table

| Flame Pin | ESP32 GPIO | Function |
|---------|------------|---------|
| 🟣 AO | 🟣 GPIO 35 | Analog Intensity |
| 🟡 DO | 🟡 GPIO 13 | Digital Alert |
| 🔴 VCC | 🔴 3.3V | Power |
| ⚫ GND | ⚫ GND | Ground |

---

## 🕵️ PIR Motion Sensor

### 📊 Pin Mapping Table

| PIR Pin | ESP32 GPIO | Function |
|-------|------------|---------|
| 🟡 OUT | 🟡 GPIO 27 | Motion Signal |
| 🔴 VCC | 🔴 5V | Power |
| ⚫ GND | ⚫ GND | Ground |

---

## 🪪 RFID Reader (RC522 – SPI)

### 📊 Pin Mapping Table

| RC522 Pin | ESP32 GPIO | Function |
|---------|------------|---------|
| 🟠 SDA / SS | 🟠 GPIO 5 | Chip Select |
| 🔵 SCK | 🔵 GPIO 18 | SPI Clock |
| 🔵 MOSI | 🔵 GPIO 23 | SPI MOSI |
| 🔵 MISO | 🔵 GPIO 19 | SPI MISO |
| 🟠 RST | 🟠 GPIO 33 | Reset |
| 🔴 VCC | 🔴 3.3V | Power |
| ⚫ GND | ⚫ GND | Ground |

📌 *RFID and LoRa share the same SPI bus but use different CS pins.*

---

## 📍 GPS Module (Neo-6M – UART)

### 📊 Pin Mapping Table

| GPS Pin | ESP32 GPIO | Function |
|-------|------------|---------|
| 🟢 TX | 🟢 GPIO 16 | UART RX |
| 🟢 RX | 🟢 GPIO 17 | UART TX |
| 🔴 VCC | 🔴 External 5V / 3.3V |
| ⚫ GND | ⚫ GND | Ground |

⚠️ Ensure correct voltage for your GPS module variant.

---

## 🔹 2. Receiver Node (Monitoring Unit – ESP32)

---

## 📡 LoRa Module (Receiver)

### 📊 Pin Mapping Table

| LoRa Pin | ESP32 GPIO |
|--------|------------|
| 🔵 SCK | 🔵 GPIO 18 |
| 🔵 MISO | 🔵 GPIO 19 |
| 🔵 MOSI | 🔵 GPIO 23 |
| 🟠 NSS | 🟠 GPIO 32 |
| 🟠 RST | 🟠 GPIO 14 |
| 🟠 DIO0 | 🟠 GPIO 4 |

---

## 🖥️ LCD Display (16×2 I2C)

### 📊 Pin Mapping Table

| LCD Pin | ESP32 GPIO | Function |
|-------|------------|---------|
| 🟢 SDA | 🟢 GPIO 21 | I2C Data |
| 🟢 SCL | 🟢 GPIO 22 | I2C Clock |
| 🔴 VCC | 🔴 5V |
| ⚫ GND | ⚫ GND |

---

## 🔔 Buzzer

### 📊 Pin Mapping Table

| Buzzer Pin | ESP32 GPIO |
|----------|------------|
| 🟡 + | 🟡 GPIO 25 |
| ⚫ − | ⚫ GND |

---

## 🧩 System Block Diagram

### 🖼️ Overall Architecture
![System Architecture](Block_Diagrams/System_Architecture.jpg)

### 🖼️ Transmitter Block Diagram
![Transmitter Block Diagram](Block_Diagrams/Transmitter_Block_Diagram.png)

### 🖼️ Receiver Block Diagram
![Receiver Block Diagram](hardware/block-diagrams/receiver_block_diagram.png)

---

## ⚠️ Important Notes

- GPIO **34 & 35 are input-only**
- Use **external power supply** for GPS and servos
- All **GND pins must be common**
- LoRa operates strictly at **3.3V**
- Avoid powering high-current devices from ESP32 3.3V pin

## ⚠️ Pin Conflict & Usage Warnings

The following points must be strictly followed to avoid hardware conflicts,
unstable behavior, or permanent damage to components.

---

### 🔴 Power & Voltage Conflicts
- **LoRa (SX1278) and RFID (RC522) MUST be powered at 3.3V only**
- Supplying **5V to LoRa or RFID will permanently damage the modules**
- High-current peripherals (GPS, ultrasonic sensor, servos) should use an
  **external 5V supply**
- All power domains must share a **common GND**

---

### 🟣 ADC / Input-Only Pins
- **GPIO 34 & GPIO 35 are input-only pins**
- Do **NOT** use these pins for:
  - Digital output
  - PWM
  - Actuators
- These pins are safe only for:
  - HC-SR04 ECHO
  - Flame sensor analog output

---

### 🔵 Shared SPI Bus (LoRa + RFID)
- LoRa and RFID **share the same SPI bus**:
  - SCK → GPIO 18
  - MOSI → GPIO 23
  - MISO → GPIO 19
- Each device uses a **separate Chip Select (CS) pin**
- Only **one CS line must be LOW at a time**
- Improper CS handling may cause:
  - Data corruption
  - SPI lockups
  - Random LoRa/RFID failures

---

### 🟢 UART Conflicts
- GPS uses **UART2 (GPIO 16 / GPIO 17)**
- Avoid using these pins for:
  - Debug UART
  - SoftwareSerial
- Debug logs should use **USB Serial (UART0)** only

---

### 🟠 Boot-Sensitive Pins (ESP32)
Avoid driving the following pins during boot:
- GPIO 0
- GPIO 2
- GPIO 12
- GPIO 15

Improper usage may cause:
- Boot failures
- Flashing errors
- ESP32 stuck in programming mode

---

### 🟡 Interrupt-Capable Pins
- LoRa **DIO0 (GPIO 4)** must support interrupts
- Do not attach multiple interrupt sources to the same GPIO
- Keep interrupt routines **short and non-blocking**

---

### 🔔 Buzzer & Output Pins
- Do not drive buzzers or relays directly from ESP32 pins without:
  - Current-limiting resistor
  - Transistor or driver module (recommended)
- Excessive current draw can cause **ESP32 brownout resets**

---

### ✅ Summary of Safe Practices
- ✔ Verify voltage levels before powering
- ✔ Share SPI carefully with CS control
- ✔ Respect input-only GPIOs
- ✔ Use external power where required
- ✔ Always share common ground

---

## ✅❌ Do / Don’t – Quick Reference

| ✅ DO | ❌ DON’T |
|------|---------|
| Power **LoRa (SX1278)** and **RFID (RC522)** with **3.3V only** | Supply **5V** to LoRa or RFID modules |
| Use **external 5V supply** for GPS, ultrasonic sensor, and servos | Power high-current devices from ESP32 3.3V pin |
| Share **common GND** between all modules | Use isolated grounds between power domains |
| Use **GPIO 34 & 35 only as inputs (ADC)** | Use GPIO 34/35 as digital output or PWM |
| Ensure only **one SPI CS line is LOW** at a time | Activate LoRa and RFID CS simultaneously |
| Keep **SPI wires short** and properly grounded | Use long, loose jumper wires for SPI |
| Use **UART2 (GPIO 16/17)** exclusively for GPS | Use GPS pins for debug serial |
| Keep **interrupt routines short** (LoRa DIO0) | Block or delay inside interrupt handlers |
| Use **current-limiting or driver circuits** for buzzers/relays | Drive high-current loads directly from ESP32 GPIO |
| Verify **voltage levels before powering ON** | Hot-plug modules while powered |
| Test each peripheral **one at a time** during bring-up | Connect all peripherals simultaneously on first power-up |
| Use **shielded or twisted wires** for SPI/UART when possible | Route SPI/UART lines near power lines |
| Double-check **pin mapping vs firmware** before flashing | Assume default ESP32 pin mappings |



---

## ✅ Summary

This combined **table + diagram** approach ensures:
- Faster wiring
- Fewer pin conflicts
- Easier debugging
- Better documentation clarity

📌 Refer to the diagrams above for physical connections.




