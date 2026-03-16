# 🏠 MMBD Home Automation System

> A smart home automation system built around MMBD sensor integration — real-time monitoring, MQTT-based device control, and automated response logic for home environments.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![MQTT](https://img.shields.io/badge/MQTT-660066?style=flat-square&logo=eclipse-mosquitto&logoColor=white)
![IoT](https://img.shields.io/badge/IoT-Embedded-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

---

## 📌 Overview

This project implements a home automation pipeline using MMBD (Multi-Modal Behavior Detection) sensors. The system reads real-time environmental data, processes it through an event-driven logic layer, and controls home devices automatically — or via manual override through a simple interface.

Built as part of coursework at NUST, but designed with real deployment architecture in mind: sensor nodes communicate over MQTT, a central broker handles routing, and a Python controller manages automation rules.

---

## 🏗️ System Architecture

```
[Sensor Nodes]
  MMBD Sensors
  Temp / Humidity
  Motion / PIR
       │
       ▼ (MQTT Publish)
[MQTT Broker]
  Mosquitto / Local Broker
       │
       ▼ (Subscribe)
[Python Controller]
  Event Processing
  Automation Rules Engine
  Threshold Logic
       │
       ├──▶ [Device Control]
       │      Lights / Fan / Relay
       │
       └──▶ [Dashboard / Logs]
              Real-time status
              Event history
```

---

## ✨ Features

- **Real-time sensor reading** — temperature, humidity, motion detection via MMBD sensors
- **MQTT communication** — publish/subscribe architecture for decoupled sensor-to-controller messaging
- **Automation rules engine** — threshold-based logic (e.g. fan ON if temp > 30°C, lights OFF if no motion for 10 min)
- **Manual override** — CLI interface to manually toggle any connected device
- **Event logging** — timestamped log of all sensor events and device state changes
- **Modular design** — easily add new sensors or devices without changing core logic

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Sensors | MMBD sensor array, DHT11/22, PIR motion sensor |
| Communication | MQTT (Mosquitto broker) |
| Controller | Python 3.x |
| Libraries | `paho-mqtt`, `RPi.GPIO` / simulation mode |
| Interface | CLI + log file output |

---

## 📁 Project Structure

```
mmbd-home-automation/
│
├── controller/
│   ├── main.py              # Entry point — starts broker listener
│   ├── automation.py        # Rules engine — threshold logic
│   ├── device_control.py    # GPIO / relay control abstraction
│   └── logger.py            # Event logging
│
├── sensors/
│   ├── mmbd_reader.py       # MMBD sensor interface
│   ├── dht_reader.py        # Temperature & humidity
│   └── motion_reader.py     # PIR motion detection
│
├── mqtt/
│   ├── publisher.py         # Sensor data publisher
│   └── subscriber.py        # Controller subscriber
│
├── config/
│   └── settings.json        # Broker address, topics, thresholds
│
├── logs/
│   └── events.log           # Auto-generated event log
│
├── requirements.txt
└── README.md
```

---

## ⚙️ Setup & Usage

### Prerequisites

```bash
pip install paho-mqtt
```

### Configuration

Edit `config/settings.json`:

```json
{
  "broker": "localhost",
  "port": 1883,
  "topics": {
    "temperature": "home/temp",
    "motion": "home/motion",
    "control": "home/control"
  },
  "thresholds": {
    "temp_high": 30,
    "motion_timeout_min": 10
  }
}
```

### Run

```bash
# Start MQTT broker (Mosquitto)
mosquitto -v

# Start sensor publishers
python sensors/mmbd_reader.py

# Start controller
python controller/main.py
```

---

## 🔁 Automation Rules (Examples)

| Condition | Action |
|-----------|--------|
| Temperature > 30°C | Turn fan ON |
| Temperature < 22°C | Turn fan OFF |
| No motion for 10 min | Turn lights OFF |
| Motion detected | Turn lights ON |
| Manual override via CLI | Bypass all rules temporarily |

---

## 📸 Demo

> *(Add a GIF or screenshot of terminal output / sensor readings here)*

---

## 🔮 Future Improvements

- [ ] Web dashboard (Flask) for remote monitoring
- [ ] Mobile app integration (Flutter)
- [ ] ML-based anomaly detection on sensor data
- [ ] Voice command support
- [ ] Multi-room expansion

---

## 👤 Author

**Abu-Bakar Chaudhary**  
Computer Engineering · NUST · Class of 2027  
[GitHub](https://github.com/abu-bakarchaudhary) · [LinkedIn](https://linkedin.com/in/abu-bakarchaudhary)
