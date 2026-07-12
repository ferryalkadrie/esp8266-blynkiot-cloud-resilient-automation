# 🏗️ System Architecture

This document describes the overall architecture of the Smart Home Automation system.

The project combines local hardware control with cloud services to provide reliable long-term operation and automatic recovery.

---

# 📦 System Components

| Component | Function |
|-----------|----------|
| ESP8266 | Main Controller |
| Blynk Cloud | Remote Monitoring & Control |
| ThingSpeak | Relay State Backup |
| Wi-Fi Router | Internet Connectivity |
| Relay Module | Electrical Load Control |
| Smartphone | User Interface |

---

# 🌐 High-Level Architecture

```
                 Smartphone
                      │
                      │
              Blynk Cloud Server
                      │
        ┌─────────────┴─────────────┐
        │                           │
        │                           │
ThingSpeak Cloud              Wi-Fi Router
        │                           │
        └─────────────┬─────────────┘
                      │
                  ESP8266
                      │
                Relay Module
                      │
             Electrical Devices
```

---

# ☁️ Cloud Communication

The ESP8266 communicates with two independent cloud services.

## Blynk Cloud

Responsible for:

- Remote control
- Mobile dashboard
- Device status
- Virtual Pins

---

## ThingSpeak

Responsible for:

- Relay state backup
- Restore after reboot
- Disaster recovery
- Long-term state storage

---

# 🔄 Relay Control Flow

```
User

↓

Blynk App

↓

Blynk Cloud

↓

ESP8266

↓

Relay Module

↓

Electrical Load
```

---

# 💾 Backup Flow

Whenever a relay changes,

the firmware stores the new relay status in ThingSpeak.

```
Relay Changed

↓

ESP8266

↓

ThingSpeak

↓

Save State
```

---

# 🔁 Recovery Flow

After every reboot,

the firmware restores the previous relay state.

```
Power ON

↓

Wi-Fi Connected

↓

ThingSpeak

↓

Download Last State

↓

Restore Relay

↓

Update Dashboard
```

---

# 📶 Dual Wi-Fi Logic

The firmware supports two Wi-Fi networks.

```
SSID 1

↓

Connected?

↓

YES

↓

Normal Operation

↓

NO

↓

SSID 2

↓

Connected?

↓

YES

↓

Continue

↓

NO

↓

Retry Automatically
```

---

# 🛡 Reliability Features

The firmware includes several protection mechanisms.

- Dual Wi-Fi Failover
- Automatic Cloud Reconnection
- ThingSpeak State Recovery
- Software Watchdog
- Periodic Connection Check
- Automatic Dashboard Synchronization

---

# ⚙ Firmware Responsibilities

The ESP8266 continuously performs the following tasks.

- Maintain Wi-Fi connection
- Process Blynk commands
- Update relay outputs
- Backup relay state
- Restore relay state
- Synchronize dashboard
- Monitor system health
- Recover from communication failures

---

# 📁 Project Structure

```
Smart-Home-Automation/

├── README.md
├── docs/
├── src/
├── images/
├── hardware/
└── LICENSE
```

---

# 🚀 Long-Term Deployment

This firmware has been designed for continuous operation.

Typical deployment includes:

- Residential Smart Home
- Lighting Automation
- Remote Relay Control
- Electrical Monitoring
- Long-Term Cloud Synchronization

---

# ✅ Architecture Summary

The architecture combines local hardware reliability with cloud synchronization.

Blynk provides real-time remote control,

while ThingSpeak ensures that relay states are preserved and automatically restored after unexpected interruptions.

Together, these services create a resilient smart home automation platform suitable for long-term unattended operation.
