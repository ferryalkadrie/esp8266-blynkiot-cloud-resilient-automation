# ☁️ ThingSpeak Configuration

This project uses **ThingSpeak** as a cloud-based state backup service.

Instead of storing only sensor data, ThingSpeak is also used to preserve the current relay status. This allows the controller to automatically restore the last known state after a power outage, unexpected reboot, or hardware replacement.

---

# 🎯 Purpose

ThingSpeak is responsible for:

- Relay state backup
- Disaster recovery
- State synchronization
- Long-term cloud storage

---

# Step 1 — Create a ThingSpeak Account

Create a ThingSpeak account and sign in.

After logging in, create a new channel.

---

# Step 2 — Create a Channel

Example configuration.

Channel Name

```
Smart Home Backup
```

Description

```
Relay State Backup
```

Enable only one field.

```
Field 1
```

Rename it to

```
RelayState
```

Save the channel.

---

# Step 3 — Obtain API Keys

Open the **API Keys** tab.

Copy the following information.

```
Channel ID
```

```
Write API Key
```

```
Read API Key
```

These values will be used inside the firmware.

---

# Step 4 — Configure Firmware

Replace the placeholders inside the source code.

```cpp
String writeApiKey = "YOUR_WRITE_API_KEY";

String readApiKey = "YOUR_READ_API_KEY";

unsigned long channelID = YOUR_CHANNEL_ID;
```

Example only.

```cpp
String writeApiKey = "ABCD123456789XYZ";
String readApiKey = "ZYX987654321ABC";
unsigned long channelID = 1234567;
```

---

# Step 5 — Data Format

The firmware stores the relay status as a binary string.

Example.

```
101100111010
```

Each digit represents one relay.

Example.

| Relay | Value |
|--------|------:|
| Relay 1 | 1 |
| Relay 2 | 0 |
| Relay 3 | 1 |
| Relay 4 | 1 |
| Relay 5 | 0 |
| Relay 6 | 0 |
| Relay 7 | 1 |
| Relay 8 | 1 |
| Relay 9 | 1 |
| Relay 10 | 0 |
| Relay 11 | 1 |
| Relay 12 | 0 |

---

# Step 6 — Upload State

Whenever a relay changes,

the firmware automatically uploads the latest binary string to ThingSpeak.

Example request.

```
https://api.thingspeak.com/update
```

The upload interval should respect ThingSpeak rate limits.

---

# Step 7 — Restore State

During startup,

the firmware requests the last stored value from ThingSpeak.

Example response.

```
101100111010
```

The controller immediately restores every relay to its previous state.

No manual intervention is required.

---

# Step 8 — Verify Operation

Open your ThingSpeak channel.

Field 1 should update automatically whenever a relay changes.

After rebooting the ESP8266,

all relay outputs should return to the previously stored state.

---

# ⚠ Notes

- Keep your API Keys private.
- Never publish your Write API Key.
- Store credentials in a separate configuration file whenever possible.
- Respect ThingSpeak upload rate limits.
- Backup your firmware before major modifications.

---

# ✅ Configuration Complete

ThingSpeak is now configured as the cloud backup service for your Smart Home Automation system.

The controller can automatically restore the previous relay state after power failures, hardware replacement, or unexpected system resets.
