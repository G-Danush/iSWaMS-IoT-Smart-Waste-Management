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
iSWaMS (IoT Smart Waste Management System) is an ESP32-based smart bin and
environmental monitoring solution designed for Smart City applications.
It combines LoRa for long-range local communication and Wi-Fi/MQTT for
cloud-based monitoring using the ThingsBoard platform.

## 🎯 Features
- Real-time bin fill level monitoring (HC-SR04)
- Environmental sensing (Temperature, Humidity, Flame)
- RFID-based user access control
- GPS-based bin location tracking
- LoRa-based long-range local communication
- MQTT-based cloud telemetry (ThingsBoard)
- Priority-based alert handling

## 🧠 System Architecture
The system consists of:
- **Transmitter Node (Smart Bin)**: ESP32 with sensors and LoRa
- **Receiver Node**: ESP32 with LCD and buzzer
- **Cloud Interface**: ThingsBoard dashboard via MQTT

## 📂 Repository Structure
```
iSWaMS-IoT-Smart-Waste-Management/
├── assets/
|   └── banner.png
|
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

## ⚙️ How to Run
1. Open the transmitter firmware in Arduino IDE.
2. Select **ESP32 Dev Module** and correct COM port.
3. Configure Wi-Fi and MQTT credentials in code.
4. Upload firmware to ESP32 transmitter.
5. Import `thingsboard-config.json` into ThingsBoard dashboard.
6. Map the `SmartBin` alias to your device.

## ☁️ ThingsBoard Dashboard
The `dashboard/thingsboard-config.json` file contains a sanitized ThingsBoard
dashboard export. It can be imported into any ThingsBoard instance without
modification.

## 📜 License
This project is licensed under the MIT License.

## 👨‍💻 Authors
- Guntupalli Danush
- Nagaraju Marella
- Saba Afreen Khatoon



