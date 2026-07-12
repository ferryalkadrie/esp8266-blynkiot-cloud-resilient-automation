# 🚀 First Boot

This document explains what happens when the ESP8266 is powered on for the very first time or after every restart.

The firmware is designed to initialize automatically without requiring user interaction.

---

# 🔋 Step 1 — Hardware Initialization

Immediately after power is applied, the firmware initializes all relay GPIO pins.

All relay outputs are set to their default safe state.

```
Relay State

↓

GPIO Initialization

↓

All Relays OFF
```

This prevents accidental relay activation during startup.

---

# 📡 Step 2 — Wi-Fi Connection

The controller attempts to connect to the configured Wi-Fi networks.

Connection order:

```
Primary Wi-Fi (SSID1)

↓

Connected?

↓

YES → Continue

↓

NO

↓

Backup Wi-Fi (SSID2)

↓

Connected?

↓

YES → Continue

↓

NO

↓

Retry Later
```

If both networks are unavailable, the firmware continues monitoring until a connection becomes available.

---

# ☁️ Step 3 — Connect to Blynk Cloud

After Wi-Fi is established, the controller connects to the Blynk Cloud server.

```
Wi-Fi Connected

↓

Blynk Authentication

↓

Device Online
```

Once connected, the device becomes available in the Blynk dashboard.

---

# 🕒 Step 4 — Synchronize Time

The firmware requests the current time from an Internet NTP server.

This ensures all scheduled operations and timestamps remain accurate.

```
Internet

↓

NTP Server

↓

ESP8266 Clock
```

---

# ☁️ Step 5 — Restore Relay State

To recover from unexpected power failures, the firmware downloads the last stored relay status from ThingSpeak.

Example.

```
ThingSpeak

↓

101100111010

↓

ESP8266

↓

Relay Restore
```

Each relay is restored to the exact state before the previous shutdown.

---

# 📱 Step 6 — Synchronize Blynk Dashboard

After restoring the relay states, the firmware updates all Blynk Virtual Pins.

```
Relay Status

↓

Virtual Pins

↓

Mobile Dashboard
```

This guarantees that the application always displays the actual hardware status.

---

# 🔄 Step 7 — Enter Normal Operation

After initialization is complete, the controller enters continuous operation.

The firmware continuously performs the following tasks:

- Process Blynk commands
- Monitor Wi-Fi connection
- Synchronize relay states
- Upload backup data to ThingSpeak
- Monitor system health
- Execute automatic recovery when necessary

---

# ⚠ Automatic Recovery

If the controller detects:

- Wi-Fi disconnection
- Cloud communication failure
- System hang
- Unexpected reboot

the firmware automatically attempts recovery without requiring manual intervention.

Recovery may include:

- Wi-Fi reconnection
- Blynk reconnection
- Relay state restoration
- Software restart

---

# ✅ Successful Startup

A successful startup sequence is shown below.

```
Power ON

↓

Initialize GPIO

↓

Connect Wi-Fi

↓

Connect Blynk

↓

Synchronize Time

↓

Restore Relay State

↓

Update Dashboard

↓

Normal Operation
```

---

# 📌 Notes

The entire startup process is fully automatic.

No manual configuration is required after power is restored, making the controller suitable for unattended long-term deployment.

---

# ✅ First Boot Complete

The controller is now ready for normal operation and continuous cloud synchronization.
