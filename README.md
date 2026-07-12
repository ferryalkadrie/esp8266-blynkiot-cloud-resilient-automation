# 💡 Automated Multichannel Lighting System with Cloud Resilience

An ultra-reliable, long-term deployed smart automation system powered by an ESP8266 controller, natively integrated with the Blynk IoT v2 platform and backended by ThingSpeak for cloud state restoration.

## 📊 Long-Term Deployment & Environmental Resilience
This codebase is not a mere proof-of-concept; it is a battle-hardened solution built for unstable real-world environments.

- **5-Year Logic Stability:** The core control logic, state syncing, and software architecture have been running flawlessly in a residential installation for **5 consecutive years**.
- **Hardware-Agnostic Portability:** Due to intense regional power surges (local grid fluctuations / PLN instability) and hardware component aging, the physical ESP8266 units require replacement roughly once a year. However, this firmware has proven to be 100% plug-and-play, completely self-recovering state values instantly on new modules without code modifications.
- **Fault-Tolerant Infrastructure:** Engineered with dual-SSID automated rollover, asynchronous state cloud backups, and a software-driven watchdog mechanism to completely mitigate local connection hang-ups.

## 🛠️ Key Architectural Strengths
- **Dual-SSID Network Recovery:** Automatically alternates between primary and backup wireless access points to prevent isolation.
- **Asynchronous Cloud State Restore:** If a sudden power spike or blackout causes a hardware reset, the controller automatically queries the latest known stable array configuration from the ThingSpeak cloud database during boot.
- **Anti-Lockup Watchdog:** A built-in logical supervisor automatically reboots the microchip if cloud or socket routines stall for more than 60 seconds.

## 🚀 Quick Setup Guide (Blynk IoT & Hardware)

To deploy this firmware on your own ESP8266 module, follow these configuration steps:

### 1. Blynk IoT Cloud Configuration
1. Log in to your **Blynk IoT Web Dashboard**.
2. Create a new **Template** (e.g., named "Multi-Channel Automation").
3. Go to the **Datastreams** tab and create 12 Virtual Pins (**V1 to V12**) as *Integer* types (Min: 0, Max: 1) to control the 12 relays.
4. Copy the `BLYNK_TEMPLATE_ID` and `BLYNK_TEMPLATE_NAME` from the info page and paste them into the very top of the `.ino` file.
5. Create a new **Device** from your template to obtain your unique `BLYNK_AUTH_TOKEN`.

### 2. Arduino IDE Environment Setup
Make sure you have the following libraries installed via the Library Manager before compiling:
- `Blynk` (Latest version supporting Blynk IoT v2)
- `ArduinoJson` (v6.x or later)
- `Time` (by Michael Margolis)

### 3. Deployment
- Open the code, change the network placeholders with your local primary/backup Wi-Fi credentials and ThingSpeak API keys.
- Flash the code to your ESP8266. The system will automatically handle the rest, including full state recovery on boot!

## 💎 Project Editions
This repository contains the **Community Edition**. For deployment-ready commercial smart building integration solutions featuring hardware-isolated optocouplers, snubber protection circuits, and industrial-grade power conditioners, please reach out to the author.
