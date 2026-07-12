# ☁️ Blynk Cloud Configuration

This project uses **Blynk IoT v2** for real-time monitoring and remote control.

## Step 1 — Create a Template

Create a new template in Blynk Console.

Example:

Template Name

```
Smart Home Automation
```

Hardware

```
ESP8266
```

Connection Type

```
WiFi
```

---

## Step 2 — Create Datastreams

Create the following Virtual Pins.

| Virtual Pin | Data Type | Min | Max |
|-------------|-----------|-----|-----|
| V1 | Integer | 0 | 1 |
| V2 | Integer | 0 | 1 |
| ... | ... | ... | ... |
| V12 | Integer | 0 | 1 |

---

## Step 3 — Create Device

Create a new device from the template.

Blynk will generate:

- BLYNK_TEMPLATE_ID
- BLYNK_TEMPLATE_NAME
- BLYNK_AUTH_TOKEN

---

## Step 4 — Configure Firmware

Open the firmware and replace the placeholders.

```cpp
#define BLYNK_TEMPLATE_ID   "YOUR_TEMPLATE_ID"
#define BLYNK_TEMPLATE_NAME "YOUR_TEMPLATE_NAME"
#define BLYNK_AUTH_TOKEN    "YOUR_AUTH_TOKEN"
```

---

## Step 5 — Configure Wi-Fi

```cpp
const char* ssid1 = "YOUR_WIFI";
const char* pass1 = "YOUR_PASSWORD";

const char* ssid2 = "BACKUP_WIFI";
const char* pass2 = "BACKUP_PASSWORD";
```

---

## Step 6 — Upload Firmware

Compile and upload the firmware to the ESP8266.

After reboot, the device will automatically connect to:

- Wi-Fi
- Blynk Cloud
- ThingSpeak

---

## Step 7 — Verify Connection

The device should appear online in the Blynk Dashboard.

You can now control all relay channels remotely.
