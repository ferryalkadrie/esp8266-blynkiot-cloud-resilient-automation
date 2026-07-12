# 💡 Automated Multichannel Smart Home Automation with Cloud State Resilience

An industrial-grade, long-term deployed smart automation system powered by an ESP8266 controller. This system is natively integrated with the modern **Blynk IoT v2** platform for real-time remote control and backed by **ThingSpeak Cloud Analytics** for asynchronous state logging and full disaster recovery restoration.

---

## 📊 Long-Term Deployment & Environmental Resilience
Unlike typical prototyping projects, this codebase is a battle-hardened solution engineered for unstable, real-world electrical and environmental conditions.

* **5-Year Production Proven:** The core control logic, state-syncing mechanisms, and network self-healing subroutines have been running flawlessly in a residential installation for **5 consecutive years** (since Day 1 of the property's grid/PLN integration).
* **Hardware-Agnostic Portability:** Due to intense local grid power surges (PLN fluctuations) and hardware aging in tropical climates, the physical ESP8266 microchips require replacement roughly once a year. This firmware is engineered to be 100% plug-and-play—allowing instant hardware migration without code modification. On boot, the new chip automatically pulls the last state from the cloud and resumes operation seamlessly.
* **Fault-Tolerant Infrastructure:** Built-in safeguards against sudden power loss, high-frequency voltage spikes, and Wi-Fi router dropouts.

---

## 🛠️ System Architecture & Key Features

### 1. Dual-SSID Network Self-Healing Engine
The system contains an automated network rollover routine. If the primary Wi-Fi access point (`ssid1`) fails or drops connection during storm conditions, the firmware instantly detects the drop within its health-check interval and switches to the backup access point (`ssid2`), maintaining 99.9% uptime.

### 2. Cloud State Backup & Restoration (Disaster Recovery)
To prevent the relays from resetting to an undesirable state after a local blackout or unexpected hardware reboot, the controller saves its current 12-channel relay matrix as a binary string (e.g., `101100111100`) directly to ThingSpeak. Upon reboot, the system handles an asynchronous REST API call to fetch this string and restore the house's lights back to their exact pre-blackout state.

### 3. Non-Blocking Debounce & API Rate Limiting
ThingSpeak imposes a strict rate limit on data updates. The firmware utilizes an event-driven, non-blocking interval supervisor (`minSendInterval = 5000`) to queue rapid physical button presses on the Blynk App and broadcast them safely without causing buffer overflows or getting blocked by the cloud server.

### 4. Hardware/Software Anti-Lockup Watchdog
Microcontrollers operating 24/7 can stall due to memory leaks or infinity loops caused by unresponsive socket handshakes. The built-in supervisor monitor tracks network responsiveness; if the system hangs or remains disconnected for more than 60 seconds, it forces a hard software-level hardware reset (`ESP.restart()`).

---

## 📌 Hardware Pin Mapping & Matrix Configuration

The firmware controls a 12-channel isolated relay module mapped across the ESP8266 GPIO layout as follows:

| Virtual Pin (Blynk v2) | Physical Hardware Pin (ESP8266) | System Load Description | Default Boot State |
| :---: | :---: | :--- | :---: |
| **V1** | `D1` | Relay Channel 1 (Main Lights) | HIGH (OFF) |
| **V2** | `D2` | Relay Channel 2 (Living Room) | HIGH (OFF) |
| **V3** | `D3` | Relay Channel 3 (Kitchen Lights) | HIGH (OFF) |
| **V4** | `D4` | Relay Channel 4 (Outdoor Fence) | HIGH (OFF) |
| **V5** | `D5` | Relay Channel 5 (Bedroom 1) | HIGH (OFF) |
| **V6** | `D6` | Relay Channel 6 (Bedroom 2) | HIGH (OFF) |
| **V7** | `D7` | Relay Channel 7 (Bathroom) | HIGH (OFF) |
| **V8** | `D8` | Relay Channel 8 (Backyard) | HIGH (OFF) |
| **V9** | `D9` | Relay Channel 9 (Auxiliary 1) | HIGH (OFF) |
| **V10** | `D10` | Relay Channel 10 (Auxiliary 2) | HIGH (OFF) |
| **V11** | `10` (GPIO10) | Relay Channel 11 (Reserved) | HIGH (OFF) |
| **V12** | `D0` | Relay Channel 12 (Master Power Switch) | HIGH (OFF) |

---

## 🚀 Step-by-Step Installation & Configuration Guide

### 1. Blynk IoT Cloud Setup
1. Log in to your **Blynk IoT Console**.
2. Create a new **Template** named `Smart Multi-Channel Automation`.
3. Navigate to the **Datastreams** tab and add 12 Virtual Pins (`V1` to `V12`) with the data type set to **Integer** (Min: `0`, Max: `1`).
4. Copy the auto-generated `BLYNK_TEMPLATE_ID` and `BLYNK_TEMPLATE_NAME` from the template info dashboard.
5. Create a new **Device** from the template to acquire your unique `BLYNK_AUTH_TOKEN`.

### 2. ThingSpeak Setup
1. Create a channel on **ThingSpeak**.
2. Enable **Field 1** to store the 12-bit string of your relay states.
3. Note down your **Channel ID**, **Write API Key**, and **Read API Key**.

### 3. Firmware Compilation
1. Open `Blynk_Home_Lighting.ino` inside the Arduino IDE.
2. Ensure you have installed the following required libraries via the Library Manager:
   * **Blynk** (Latest Version supporting IoT v2)
   * **ArduinoJson** (v6.x or newer)
   * **Time** (by Michael Margolis)
3. Paste your template credentials at the very top of the script:
   ```cpp
   #define BLYNK_TEMPLATE_ID   "YOUR_TEMPLATE_ID"
   #define BLYNK_TEMPLATE_NAME "YOUR_TEMPLATE_NAME"
