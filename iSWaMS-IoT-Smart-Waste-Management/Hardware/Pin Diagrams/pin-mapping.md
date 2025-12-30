\# 📌 Pin Mapping – iSWaMS IoT Smart Waste Management System



This document presents the \*\*pin configuration\*\* for the iSWaMS project, combining

\*\*clear tables\*\* with \*\*visual wiring/block diagrams\*\* for easier understanding

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

  - GPS Module (Neo-6M, via regulator)

- **External Supply**

  - Used for GPS and high-current peripherals

  - Grounds are shared with ESP32 (common GND)

⚠️ LoRa and RFID **must NOT** be powered from 5V.



---



\## 🔹 1. Transmitter Node (Smart Bin – ESP32)



\### 🧠 ESP32 Dev Module

\- Logic Level: \*\*3.3V\*\*

\- Shared SPI Bus: \*\*LoRa + RFID\*\*

\- UART used for \*\*GPS\*\*



---



\## 📡 LoRa Module (Ra-02 / SX1278)



\### 📊 Pin Mapping Table



| LoRa Pin | ESP32 GPIO | Function |

|--------|------------|---------|

| VCC | 3.3V | Power |

| GND | GND | Ground |

| SCK | GPIO 18 | SPI Clock |

| MISO | GPIO 19 | SPI MISO |

| MOSI | GPIO 23 | SPI MOSI |

| NSS | GPIO 32 | Chip Select |

| RST | GPIO 14 | Reset |

| DIO0 | GPIO 4 | Interrupt |



\### 🖼️ Diagram

!\[LoRa Wiring Diagram](pin-diagrams/iSWaMS\_Transmitter\_Diagram.jpg)



---



\## 📏 Ultrasonic Sensor (HC-SR04)



\### 📊 Pin Mapping Table



| HC-SR04 Pin | ESP32 GPIO | Function |

|-----------|------------|---------|

| VCC | 5V | Power |

| GND | GND | Ground |

| TRIG | GPIO 25 | Trigger |

| ECHO | GPIO 34 | Echo (Input only) |



\### 🖼️ Diagram

!\[HC-SR04 Wiring](pin-diagrams/iSWaMS\_Transmitter\_Diagram.jpg)



---



\## 🌡️ Temperature \& Humidity Sensor (DHT22)



\### 📊 Pin Mapping Table



| DHT22 Pin | ESP32 GPIO | Function |

|---------|------------|---------|

| VCC | 3.3V | Power |

| DATA | GPIO 26 | Data |

| GND | GND | Ground |



---



\## 🔥 Flame Sensor



\### 📊 Pin Mapping Table



| Flame Pin | ESP32 GPIO | Function |

|---------|------------|---------|

| AO | GPIO 35 | Analog Intensity |

| DO | GPIO 13 | Digital Alert |

| VCC | 3.3V | Power |

| GND | GND | Ground |



---



\## 🕵️ PIR Motion Sensor



\### 📊 Pin Mapping Table



| PIR Pin | ESP32 GPIO | Function |

|-------|------------|---------|

| OUT | GPIO 27 | Motion Signal |

| VCC | 5V | Power |

| GND | GND | Ground |



---



\## 🪪 RFID Reader (RC522 – SPI)



\### 📊 Pin Mapping Table



| RC522 Pin | ESP32 GPIO | Function |

|---------|------------|---------|

| SDA / SS | GPIO 5 | Chip Select |

| SCK | GPIO 18 | SPI Clock |

| MOSI | GPIO 23 | SPI MOSI |

| MISO | GPIO 19 | SPI MISO |

| RST | GPIO 33 | Reset |

| VCC | 3.3V | Power |

| GND | GND | Ground |



📌 \*RFID and LoRa share the same SPI bus but use different CS pins.\*



---



\## 📍 GPS Module (Neo-6M – UART)



\### 📊 Pin Mapping Table



| GPS Pin | ESP32 GPIO | Function |

|-------|------------|---------|

| TX | GPIO 16 | UART RX |

| RX | GPIO 17 | UART TX |

| VCC | External 5V / 3.3V |

| GND | GND | Ground |



⚠️ Ensure correct voltage for your GPS module variant.



---



\## 🔹 2. Receiver Node (Monitoring Unit – ESP32)



---



\## 📡 LoRa Module (Receiver)



\### 📊 Pin Mapping Table



| LoRa Pin | ESP32 GPIO |

|--------|------------|

| SCK | GPIO 18 |

| MISO | GPIO 19 |

| MOSI | GPIO 23 |

| NSS | GPIO 32 |

| RST | GPIO 14 |

| DIO0 | GPIO 4 |



\### 🖼️ Diagram

!\[Receiver LoRa Wiring](pin-diagrams/iSWaMS\_Receiver\_Diagram.jpg)



---



\## 🖥️ LCD Display (16×2 I2C)



\### 📊 Pin Mapping Table



| LCD Pin | ESP32 GPIO | Function |

|-------|------------|---------|

| SDA | GPIO 21 | I2C Data |

| SCL | GPIO 22 | I2C Clock |

| VCC | 5V |

| GND | GND |



---



\## 🔔 Buzzer



\### 📊 Pin Mapping Table



| Buzzer Pin | ESP32 GPIO |

|----------|------------|

| + | GPIO 25 |

| − | GND |



---



\## 🧩 System Block Diagram



\### 🖼️ Overall Architecture

!\[System Architecture](block-diagrams/system\_architecture.jpg)



\### 🖼️ Transmitter Block Diagram

!\[Transmitter Block Diagram](block-diagrams/Transmitter\_block\_diagram.png)



\### 🖼️ Receiver Block Diagram

!\[Receiver Block Diagram](block-diagrams/Receiver\_block\_diagram.png)



---



\## ⚠️ Important Notes



\- GPIO \*\*34 \& 35 are input-only\*\*

\- Use \*\*external power supply\*\* for GPS and servos

\- All \*\*GND pins must be common\*\*

\- LoRa operates strictly at \*\*3.3V\*\*

\- Avoid powering high-current devices from ESP32 3.3V pin



---



\## ✅ Summary



This combined \*\*table + diagram\*\* approach ensures:

\- Faster wiring

\- Fewer pin conflicts

\- Easier debugging

\- Better documentation clarity



📌 Refer to the diagrams above for physical connections.





This document presents the \*\*pin configuration\*\* for the iSWaMS project, combining

\*\*clear tables\*\* with \*\*visual wiring/block diagrams\*\* for easier understanding

and faster hardware setup.



---



\## 🔹 1. Transmitter Node (Smart Bin – ESP32)



\### 🧠 ESP32 Dev Module

\- Logic Level: \*\*3.3V\*\*

\- Shared SPI Bus: \*\*LoRa + RFID\*\*

\- UART used for \*\*GPS\*\*



---



\## 📡 LoRa Module (Ra-02 / SX1278)



\### 📊 Pin Mapping Table



| LoRa Pin | ESP32 GPIO | Function |

|--------|------------|---------|

| VCC | 3.3V | Power |

| GND | GND | Ground |

| SCK | GPIO 18 | SPI Clock |

| MISO | GPIO 19 | SPI MISO |

| MOSI | GPIO 23 | SPI MOSI |

| NSS | GPIO 32 | Chip Select |

| RST | GPIO 14 | Reset |

| DIO0 | GPIO 4 | Interrupt |



\### 🖼️ Diagram

!\[LoRa Wiring Diagram](pin-diagrams/iSWaMS\_Transmitter\_Diagram.jpg)



---



\## 📏 Ultrasonic Sensor (HC-SR04)



\### 📊 Pin Mapping Table



| HC-SR04 Pin | ESP32 GPIO | Function |

|-----------|------------|---------|

| VCC | 5V | Power |

| GND | GND | Ground |

| TRIG | GPIO 25 | Trigger |

| ECHO | GPIO 34 | Echo (Input only) |



\### 🖼️ Diagram

!\[HC-SR04 Wiring](pin-diagrams/iSWaMS\_Transmitter\_Diagram.jpg)



---



\## 🌡️ Temperature \& Humidity Sensor (DHT22)



\### 📊 Pin Mapping Table



| DHT22 Pin | ESP32 GPIO | Function |

|---------|------------|---------|

| VCC | 3.3V | Power |

| DATA | GPIO 26 | Data |

| GND | GND | Ground |



---



\## 🔥 Flame Sensor



\### 📊 Pin Mapping Table



| Flame Pin | ESP32 GPIO | Function |

|---------|------------|---------|

| AO | GPIO 35 | Analog Intensity |

| DO | GPIO 13 | Digital Alert |

| VCC | 3.3V | Power |

| GND | GND | Ground |



---



\## 🕵️ PIR Motion Sensor



\### 📊 Pin Mapping Table



| PIR Pin | ESP32 GPIO | Function |

|-------|------------|---------|

| OUT | GPIO 27 | Motion Signal |

| VCC | 5V | Power |

| GND | GND | Ground |



---



\## 🪪 RFID Reader (RC522 – SPI)



\### 📊 Pin Mapping Table



| RC522 Pin | ESP32 GPIO | Function |

|---------|------------|---------|

| SDA / SS | GPIO 5 | Chip Select |

| SCK | GPIO 18 | SPI Clock |

| MOSI | GPIO 23 | SPI MOSI |

| MISO | GPIO 19 | SPI MISO |

| RST | GPIO 33 | Reset |

| VCC | 3.3V | Power |

| GND | GND | Ground |



📌 \*RFID and LoRa share the same SPI bus but use different CS pins.\*



---



\## 📍 GPS Module (Neo-6M – UART)



\### 📊 Pin Mapping Table



| GPS Pin | ESP32 GPIO | Function |

|-------|------------|---------|

| TX | GPIO 16 | UART RX |

| RX | GPIO 17 | UART TX |

| VCC | External 5V / 3.3V |

| GND | GND | Ground |



⚠️ Ensure correct voltage for your GPS module variant.



---



\## 🔹 2. Receiver Node (Monitoring Unit – ESP32)



---



\## 📡 LoRa Module (Receiver)



\### 📊 Pin Mapping Table



| LoRa Pin | ESP32 GPIO |

|--------|------------|

| SCK | GPIO 18 |

| MISO | GPIO 19 |

| MOSI | GPIO 23 |

| NSS | GPIO 32 |

| RST | GPIO 14 |

| DIO0 | GPIO 4 |



\### 🖼️ Diagram

!\[Receiver LoRa Wiring](pin-diagrams/iSWaMS\_Receiver\_Diagram.jpg)



---



\## 🖥️ LCD Display (16×2 I2C)



\### 📊 Pin Mapping Table



| LCD Pin | ESP32 GPIO | Function |

|-------|------------|---------|

| SDA | GPIO 21 | I2C Data |

| SCL | GPIO 22 | I2C Clock |

| VCC | 5V |

| GND | GND |



---



\## 🔔 Buzzer



\### 📊 Pin Mapping Table



| Buzzer Pin | ESP32 GPIO |

|----------|------------|

| + | GPIO 25 |

| − | GND |



---



\## 🧩 System Block Diagram



\### 🖼️ Overall Architecture

!\[System Architecture](block-diagrams/system\_architecture.jpg)



\### 🖼️ Transmitter Block Diagram

!\[Transmitter Block Diagram](block-diagrams/Transmitter\_block\_diagram.png)



\### 🖼️ Receiver Block Diagram

!\[Receiver Block Diagram](block-diagrams/Receiver\_block\_diagram.png)



---



\## ⚠️ Important Notes



\- GPIO \*\*34 \& 35 are input-only\*\*

\- Use \*\*external power supply\*\* for GPS and servos

\- All \*\*GND pins must be common\*\*

\- LoRa operates strictly at \*\*3.3V\*\*

\- Avoid powering high-current devices from ESP32 3.3V pin



---



\## ✅ Summary



This combined \*\*table + diagram\*\* approach ensures:

\- Faster wiring

\- Fewer pin conflicts

\- Easier debugging

\- Better documentation clarity



📌 Refer to the diagrams above for physical connections.



