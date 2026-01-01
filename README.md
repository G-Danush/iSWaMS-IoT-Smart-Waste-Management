# iSWaMS-IoT-Smart-Waste-Management

![Platform](https://img.shields.io/badge/Platform-ESP32-blue)
![RTOS](https://img.shields.io/badge/RTOS-FreeRTOS-lightgrey)
![Hardware](https://img.shields.io/badge/Hardware-ESP32%20%7C%20SX1278%20%7C%20HC--SR04%20%7C%20DHT22%20%7C%20GPS-blue)
![RFID](https://img.shields.io/badge/RFID-RC522-important)
![Sensors](https://img.shields.io/badge/Sensors-Flame%20%7C%20PIR-yellow)
![Display](https://img.shields.io/badge/Display-16x2%20I2C%20LCD-informational)

![LoRa Frequency](https://img.shields.io/badge/LoRa-433MHz-green)
![LoRa Range](https://img.shields.io/badge/Range-1--2km%20(LoS)-success)

![Protocol](https://img.shields.io/badge/MQTT-Enabled-orange)
![Cloud](https://img.shields.io/badge/Cloud-ThingsBoard-blueviolet)
![Language](https://img.shields.io/badge/Language-C%2B%2B-brightgreen)
![IDE](https://img.shields.io/badge/IDE-Arduino-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Build Status](https://img.shields.io/github/actions/workflow/status/G-Danush/iSWaMS-IoT-Smart-Waste-Management/arduino-build.yml?branch=main)

![GitHub repo size](https://img.shields.io/github/repo-size/G-Danush/iSWaMS-IoT-Smart-Waste-Management)
![GitHub last commit](https://img.shields.io/github/last-commit/G-Danush/iSWaMS-IoT-Smart-Waste-Management)
![GitHub stars](https://img.shields.io/github/stars/G-Danush/iSWaMS-IoT-Smart-Waste-Management?style=social)


## 📌 Overview
**iSWaMS (IoT Smart Waste Management System)** is an ESP32-based intelligent waste monitoring and environmental safety system designed for smart city applications.  
The system integrates **LoRa for long-range local communication** and **Wi-Fi/MQTT for cloud connectivity** using the **ThingsBoard IoT platform**.

It continuously monitors **bin fill levels, environmental conditions, fire hazards, motion activity, RFID-based access, and GPS location**, ensuring efficient waste collection, improved safety, and real-time remote visualization.

---

## 🎯 Objectives
- Optimize waste collection logistics
- Prevent bin overflow and fire hazards
- Enable secure and traceable waste disposal using RFID
- Provide real-time local and cloud-based monitoring
- Demonstrate a scalable Smart City IoT architecture

---

## 🧠 System Architecture

### 1️⃣ Transmitter Node (Smart Bin)
- **Controller:** ESP32 (30-pin Dev Module)
- **Sensors:**
  - HC-SR04 – Bin fill level
  - DHT22 – Temperature & Humidity
  - Flame Sensor – Fire detection (Analog & Digital)
  - PIR – Motion detection
  - GPS (Neo-6M) – Location tracking
  - RFID (RC522) – User authentication
- **Communication:**
  - LoRa (Ra-02 / SX1278) – Local transmission
  - Wi-Fi + MQTT – Cloud telemetry
- **Actuators & Indicators:**
  - PCA9685 – PWM expansion (servo-ready)
  - Status LED

---

### 2️⃣ Receiver Node (Monitoring Station)
- ESP32 with LoRa receiver
- 16×2 I2C LCD display
- Buzzer for alert indication
- Priority-based alert display logic

---

### 3️⃣ Cloud Interface
- **Platform:** ThingsBoard
- **Protocol:** MQTT
- **Features:**
  - Real-time dashboards
  - Historical data logging
  - Alert visualization
  - GPS map tracking

---

## 🔄 Data Transmission Strategy
To overcome the **255-byte LoRa payload limitation**, the system implements a **cyclic transmission protocol**:

| Sequence | Data Packet |
|--------|------------|
| Seq 0 | GPS (Latitude, Longitude, Fix status) |
| Seq 1 | Environment (Temp, Humidity, Flame) |
| Seq 2 | Bin Data (Distance, Fill %, Motion) |
| Seq 3 | RFID (UID, Entry/Exit, User count) |
| Seq 4 | System Health |

⚠️ **Critical alerts** (Fire, Bin Full, Motion, High Temp, RFID events) are injected into **every LoRa packet** for immediate detection.

---

## ☁️ MQTT Telemetry
- Aggregates all sensor data into a **single JSON mega-payload**
- Publishes to: **v1/devices/me/telemetry**

- Optimized using:
- `ArduinoJson`
- Increased MQTT buffer size (1024 bytes)

---

## 📊 Dashboard Features (ThingsBoard)
- Bin fill percentage indicator
- Temperature & Humidity gauges
- Flame intensity monitoring
- Alert status panels
- GPS location mapping

---

## 🗂️ Repository Structure
```
iSWaMS-IoT-Smart-Waste-Management/
├── dashboard/
│   └── cps_swams_dashboard.json
|
├── docs/
│   ├── IEEE_Format_IoT_SWaMS.pdf
│   ├── SWaMS_CPS_Project_PPT_Rev3_9-Dec-2025.pptx
│   └── SWaMS_IoT_Project_PPT_Rev2_9-Dec-2025.pptx
|
├── firmware/
│   ├── receiver/
│   │   ├── receiver.ino
│   │   └── receiver.txt
│   └── transmitter/
│       ├── transmitter.ino
│       └── transmitter.txt
|
├── hardware/
│   ├── block-diagrams/
│   │   ├── receiver_block_diagram.png
│   │   ├── system_architecture.jpg
│   │   └── transmitter_block_diagram.png
│   └── pin-diagrams/
│       ├── iSWaMS_receiver_Diagram.jpg
│       ├── iSWaMS_transmitter_Diagram.jpg
│       └── pin_mapping.md
|
├── ML_data/
│   ├── README.md
│   ├── SWaMS_VRP_11DEC2025.html
│   ├── VRP_Whatsapp_test1.html 
│   ├── google_links.csv
│   ├── optimized_routes.csv
│   ├── optimized_routes_map.html 
│   └── smart_waste_ml_and_vrp.html
|
├── README.md
├── .gitignore
└── LICENSE

```

---

## 🧪 Key Challenges Addressed
- LoRa bandwidth limitation using cyclic packets
- Shared SPI bus stability (RFID + LoRa)
- Power instability due to high current modules
- GPS cold-start delays
- Concurrent handling of Wi-Fi, LoRa, and sensors
- RFID state consistency with timeout handling

---

## 🛠️ Technologies Used
- **Hardware:** ESP32, SX1278 (LoRa), Neo-6M GPS
- **Protocols:** LoRa, MQTT, SPI, I2C, UART
- **Cloud:** ThingsBoard
- **Firmware:** Arduino (ESP32), FreeRTOS concepts
- **Libraries:** ArduinoJson, PubSubClient, TinyGPS++

---

## 📦 Deliverables
- Smart Bin prototype (Transmitter)
- Receiver monitoring unit
- Optimized ESP32 firmware
- Real-time IoT dashboard
- IEEE-formatted project documentation

---

## 🚀 Future Enhancements
- Predictive waste collection using ML
- Mobile app integration
- Solar-powered deployment
- Multi-bin network scaling
- Secure OTA firmware updates

---

## 👨‍💻 Authors
- **Guntupalli Danush**
- **Nagaraju Marella**
- **Saba Afreen Khatoon**

Department of IoT & Autonomous Systems  
Indian Institute of Information Technology, Sri City, Chittoor

---

## 📜 License
This project is licensed under the **MIT License** – feel free to use, modify, and distribute with attribution.

---

## ⭐ Acknowledgment
Special thanks to faculty mentors and the Electronics Department of IIIT Sri City for their guidance and support.

---

> 📌 *This repository is intended for academic, learning, and prototype demonstration purposes.*
