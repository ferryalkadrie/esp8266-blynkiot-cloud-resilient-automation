# 🔌 Hardware Wiring

This project is built around an ESP8266 microcontroller controlling a 12-channel relay board with cloud connectivity through Wi-Fi.

---

# 📦 Hardware Components

| Component | Quantity |
|-----------|---------:|
| ESP8266 Development Board | 1 |
| 12-Channel Relay Module | 1 |
| 5V Power Supply | 1 |
| Wi-Fi Router | 1 |
| AC Loads (Lights, Fans, etc.) | As Required |

---

# 📍 GPIO Mapping

| GPIO | Relay | Blynk Virtual Pin |
|------|-------|-------------------|
| D1 | Relay 1 | V1 |
| D2 | Relay 2 | V2 |
| D3 | Relay 3 | V3 |
| D4 | Relay 4 | V4 |
| D5 | Relay 5 | V5 |
| D6 | Relay 6 | V6 |
| D7 | Relay 7 | V7 |
| D8 | Relay 8 | V8 |
| RX | Relay 9 | V9 |
| TX | Relay 10 | V10 |
| GPIO10 | Relay 11 | V11 |
| D0 | Relay 12 | V12 |

---

# 🔋 Power Supply

Power the ESP8266 using a stable **5V USB power supply**.

The relay module should be powered from a regulated power source capable of supplying sufficient current for all active relay channels.

---

# 🌐 Network Connection

The ESP8266 connects to:

- Primary Wi-Fi Network (SSID1)
- Secondary Backup Wi-Fi Network (SSID2)

The firmware automatically switches to the backup network if the primary connection becomes unavailable.

---

# 🖼 Wiring Diagram

Place the wiring diagram in:

```
images/wiring.png
```

Then display it inside this document.

```html
<p align="center">
    <img src="../images/wiring.png" width="850">
</p>
```

---

# ⚠ Notes

- Double-check all wiring before applying power.
- Never connect mains AC directly to the ESP8266.
- Use opto-isolated relay modules whenever possible.
- Verify GPIO assignments before uploading firmware.

---

# ✅ Hardware Wiring Complete

The controller is now ready for firmware upload and cloud configuration.
