# ❓ Frequently Asked Questions (FAQ)

This document answers the most common questions about the project.

---

# 1. Can I use another ESP8266 board?

Yes.

The firmware can run on most ESP8266 development boards.

Example:

- NodeMCU
- Wemos D1 Mini
- ESP-12E
- ESP-12F

Some GPIO assignments may need adjustment depending on your hardware.

---

# 2. Does the project require Blynk?

Yes.

Remote monitoring and relay control are performed through the Blynk IoT Cloud.

---

# 3. Why is ThingSpeak used?

ThingSpeak stores the last relay status.

If power is lost or the controller is replaced, the firmware downloads the latest relay state and restores all outputs automatically.

---

# 4. Can the project work without ThingSpeak?

Yes.

However, automatic relay state recovery after reboot will not be available.

---

# 5. Why are two Wi-Fi networks configured?

The firmware supports automatic failover.

If the primary Wi-Fi becomes unavailable, the controller attempts to connect to the backup network.

---

# 6. Does the firmware reconnect automatically?

Yes.

The firmware continuously checks:

- Wi-Fi connection
- Blynk connection
- Internet availability

Recovery is performed automatically whenever possible.

---

# 7. What happens after a power outage?

The startup sequence is:

```
Power ON

↓

Connect Wi-Fi

↓

Connect Blynk

↓

Read ThingSpeak

↓

Restore Relay State

↓

Update Dashboard

↓

Ready
```

The previous relay status is restored automatically if a valid backup exists.

---

# 8. How many relay channels are supported?

This project controls:

```
12 Relay Outputs
```

Each relay is assigned to its own Blynk Virtual Pin.

---

# 9. Is this project suitable for long-term operation?

Yes.

The firmware includes:

- Automatic Wi-Fi recovery
- Automatic cloud reconnection
- Software watchdog
- Relay state backup
- Relay state restoration

These features are intended to improve reliability during continuous operation.

---

# 10. Can I modify the firmware?

Yes.

The project is intended as a reference for learning and customization.

You may adapt:

- GPIO mapping
- Number of relays
- Cloud services
- User interface
- Automation logic

to suit your own application.

---

# 11. Why are credentials not included?

Sensitive information such as:

- Wi-Fi passwords
- Blynk Auth Tokens
- ThingSpeak API Keys

has been intentionally removed to protect privacy and security.

Users should provide their own credentials before compiling the firmware.

---

# 12. Where can I find the wiring diagram?

The wiring diagram is available in the **images/** directory.

Example:

```
images/wiring.png
```

---

# 13. What Arduino libraries are required?

Install the latest compatible versions of:

- Blynk
- ArduinoJson
- Time
- ESP8266 Board Package

Additional libraries may be required if new hardware features are added.

---

# 14. Is this project beginner-friendly?

Basic knowledge of:

- Arduino IDE
- ESP8266
- Wi-Fi networking
- Blynk IoT

is recommended before modifying the firmware.

---

# 📌 Need More Help?

If your issue is not covered here, refer to:

- README.md
- Hardware_Wiring.md
- Firmware_Compilation.md
- Troubleshooting.md

These documents provide detailed setup and debugging information.

---

# ✅ FAQ Complete

Thank you for exploring this project.

We hope this documentation helps you understand, deploy, and customize the system successfully.
