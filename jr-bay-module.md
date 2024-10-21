# Custom JR Bay Transmitter

Now you saw two communication protocols: **UDP** and the good old receivers. I was planning to make a custom JR bay transmitter that uses **ESP-NOW**. It uses the radio chip of ESP32 but with a modulation similar to **LoRa** modulation, as used by **ExpressLRS (ELRS)**, to obtain higher ranges.

In this guide, we will explore creating a custom **JR bay transmitter** using ESP32 that leverages the ESP32’s radio chip and utilizes LoRa-like modulation for achieving higher communication ranges. This approach combines the flexibility of **ESP-NOW** with long-range communication, making it ideal for robust control systems.

## 1. ESP-NOW Communication Protocol

**ESP-NOW** is a wireless communication protocol by Espressif that allows for fast, low-power, peer-to-peer communication without the need for Wi-Fi. It's an excellent base protocol for real-time control systems like custom JR bay transmitters.

### ESP-NOW Documentation:

- [ESP-NOW Official Documentation](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/network/esp_now.html)

### ESP-NOW Library for Arduino:

- I have developed a library for ESP-NOW specifically for Arduino that simplifies the integration of this protocol into your projects:
  - [ESP-NOW Arduino Library](https://github.com/yoursunny/WifiEspNow)

## 2. Using LoRa-Like Modulation with ESP32

The ESP32 supports modulation techniques that can be adapted to work similarly to **LoRa** for increasing the communication range. By modifying the existing communication protocols like ESP-NOW and adding modulation features, we can achieve longer ranges similar to the **ELRS** system.

### Steps:

- Implement **LoRa-like modulation** with the **ESP32 radio chip** by adjusting the bandwidth and spreading factor settings.
- Modify the communication protocol to accommodate long-range transmission with minimal interference, inspired by ELRS modulation techniques.

## 3. JR Bay Module with EdgeTX

To integrate your custom transmitter into the RC world, it must be compatible with JR bay systems, which are commonly used in radios like **EdgeTX**.

### EdgeTX Documentation for JR Bay Modules:

EdgeTX provides extensive support for JR bay modules, which can help you design a compatible system that works seamlessly with your custom ESP32-based JR bay transmitter.

- [EdgeTX JR Bay Documentation](https://edgetx.org/Radio-hardware-specifications-for-EdgeTX/)

## Summary

By combining **ESP-NOW** with **LoRa-like modulation** and integrating it into a **custom JR bay transmitter**, you can create a powerful and flexible long-range communication system. The transmitter will leverage the ESP32’s radio chip and be compatible with **EdgeTX**-based radios, offering a customizable and open-source solution for RC enthusiasts.

- **ESP-NOW Documentation**: [ESP-NOW Docs](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/network/esp_now.html)
- **ESP-NOW Library for Arduino**: [ESP-NOW Arduino Library](https://github.com/yoursunny/WifiEspNow)
- **EdgeTX JR Bay Documentation**: [EdgeTX JR Bay Docs](https://github.com/EdgeTX/edgetx/wiki/JR-Bay-Module)
