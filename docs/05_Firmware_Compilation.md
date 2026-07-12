# 💻 Firmware Compilation

This document explains how to compile and upload the firmware to the ESP8266 using the Arduino IDE.

---

# 📋 Requirements

Before compiling the project, install the following software.

- Arduino IDE 2.x or newer
- ESP8266 Board Package
- USB Driver for your development board

---

# 📦 Required Libraries

Install these libraries from the Arduino Library Manager.

| Library | Recommended Version |
|----------|--------------------:|
| Blynk | Latest |
| ArduinoJson | Version 6.x |
| Time | Latest |

---

# 📥 Install ESP8266 Board Package

Open:

```
File
↓

Preferences
```

Add the following Boards Manager URL.

```
https://arduino.esp8266.com/stable/package_esp8266com_index.json
```

Then open:

```
Tools

↓

Board

↓

Boards Manager
```

Search for:

```
ESP8266
```

Install the latest stable version.

---

# ⚙ Board Configuration

Select the appropriate board.

Example:

```
Board

NodeMCU 1.0 (ESP-12E Module)
```

Recommended settings.

| Option | Value |
|---------|-------|
| CPU Frequency | 80 MHz |
| Flash Size | 4MB |
| Upload Speed | 115200 |
| Flash Mode | DIO |

---

# 🔑 Configure Credentials

Replace the placeholder credentials.

```cpp
#define BLYNK_AUTH_TOKEN "YOUR_AUTH_TOKEN"

const char* ssid1 = "YOUR_WIFI";
const char* pass1 = "YOUR_PASSWORD";

const char* ssid2 = "YOUR_BACKUP_WIFI";
const char* pass2 = "YOUR_BACKUP_PASSWORD";
```

Also replace your ThingSpeak API Keys.

```cpp
const char* writeAPIKey = "YOUR_WRITE_API_KEY";
const char* readAPIKey  = "YOUR_READ_API_KEY";
const char* channelID   = "YOUR_CHANNEL_ID";
```

---

# 🔌 Upload Firmware

Connect the ESP8266 to your computer using a USB cable.

Select the correct COM Port.

```
Tools

↓

Port

↓

COMx
```

Click:

```
Upload
```

Wait until the upload process finishes successfully.

---

# ✅ First Boot

After booting,

the firmware will automatically:

- Connect to Wi-Fi
- Connect to Blynk Cloud
- Synchronize RTC
- Restore relay states from ThingSpeak
- Synchronize all Blynk widgets

---

# 🛠 Troubleshooting

## Cannot connect to Wi-Fi

- Verify SSID and password.
- Ensure the router is operating normally.

---

## Upload Failed

- Verify the USB cable supports data transfer.
- Install the correct USB driver.
- Select the correct COM port.

---

## Device Offline in Blynk

- Verify the Auth Token.
- Check the internet connection.
- Confirm that the Blynk server is reachable.

---

## ThingSpeak Restore Failed

- Verify the Channel ID.
- Verify the Read API Key.
- Ensure the channel is public or accessible using the provided API Key.

---

# ✅ Firmware Compilation Complete

The firmware is now ready for long-term deployment.
