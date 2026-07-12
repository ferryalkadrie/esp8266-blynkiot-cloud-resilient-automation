# 🛠 Troubleshooting

This document provides solutions to the most common issues encountered during installation and long-term operation.

---

# 📶 Wi-Fi Connection Failed

## Symptoms

- Device cannot connect to Wi-Fi.
- Device remains offline.
- Blynk never becomes online.

## Possible Causes

- Incorrect SSID
- Incorrect password
- Router unavailable
- Weak Wi-Fi signal

## Solutions

- Verify Wi-Fi credentials.
- Restart the router.
- Move the device closer to the router.
- Check whether the backup Wi-Fi network is available.

---

# ☁️ Blynk Device Offline

## Symptoms

- Device shows Offline in Blynk.
- Mobile App cannot control relays.

## Possible Causes

- Internet connection lost.
- Invalid Auth Token.
- Temporary Blynk Cloud interruption.

## Solutions

- Verify Internet connectivity.
- Confirm the correct BLYNK_AUTH_TOKEN.
- Restart the ESP8266 if necessary.
- Wait a few minutes if Blynk Cloud is under maintenance.

---

# 📡 ThingSpeak Update Failed

## Symptoms

- Relay status is not saved.
- Previous relay state cannot be restored.

## Possible Causes

- Incorrect API Key.
- Invalid Channel ID.
- Internet unavailable.
- Rate limit exceeded.

## Solutions

- Verify Write API Key.
- Verify Read API Key.
- Confirm the Channel ID.
- Avoid sending updates too frequently.

---

# 🔄 Relay State Not Restored

## Symptoms

- All relays return to OFF after reboot.

## Possible Causes

- No backup exists in ThingSpeak.
- ThingSpeak request failed.
- Invalid relay status string.

## Solutions

- Check whether Field 1 contains relay data.
- Verify Read API Key.
- Test the ThingSpeak API manually.
- Ensure Internet connectivity during startup.

---

# 💻 Firmware Upload Failed

## Symptoms

- Upload error.
- Timeout.
- Failed to connect to ESP8266.

## Solutions

- Use a USB cable that supports data transfer.
- Install the correct USB driver.
- Select the correct COM port.
- Press the RESET button before uploading if required.

---

# ⚡ Random Restart

## Symptoms

- Device restarts unexpectedly.

## Possible Causes

- Unstable power supply.
- Brownout.
- Insufficient USB current.

## Solutions

- Use a regulated 5V power supply.
- Avoid powering relays directly from the ESP8266.
- Use adequate wiring and power capacity.

---

# 📱 Dashboard Not Updating

## Symptoms

- Relay changes are not reflected in the Blynk App.

## Possible Causes

- Lost Internet connection.
- Virtual Pins not synchronized.

## Solutions

- Verify Wi-Fi connection.
- Restart the Blynk application.
- Restart the ESP8266 if synchronization fails.

---

# 🌐 Dual Wi-Fi Not Switching

## Symptoms

- Device never connects to the backup network.

## Possible Causes

- Backup SSID incorrect.
- Backup password incorrect.
- Backup router unavailable.

## Solutions

- Verify SSID2 configuration.
- Verify Password2.
- Confirm that the backup network is operational.

---

# 🛡 Watchdog Restart

## Symptoms

Serial Monitor displays:

```
System hang > 1 minute...
Restarting...
```

This behavior is expected.

The watchdog automatically restarts the firmware when it detects that the controller has stopped responding.

No user action is normally required.

---

# 📋 Serial Monitor Messages

Typical startup sequence:

```
Program Started

↓

Connecting Wi-Fi...

↓

Wi-Fi Connected

↓

Connecting Blynk...

↓

Connected

↓

Restoring Relay State...

↓

Ready
```

This indicates normal operation.

---

# ❓ Still Having Problems?

Before reporting an issue, verify:

- Wi-Fi credentials
- Blynk configuration
- ThingSpeak configuration
- Internet connection
- Power supply stability
- Board selection
- Required libraries

Most problems are caused by configuration errors rather than firmware issues.

---

# ✅ Troubleshooting Complete

If all configuration steps have been followed correctly, the firmware is designed to recover automatically from most network interruptions without requiring user intervention.
