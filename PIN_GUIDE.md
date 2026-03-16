# PIN Code System Guide

This document explains the purpose of the different PIN codes used in the Easy Wallbox integration.

---

## 1. BLE Pairing PIN (Passkey)

**Usage:**
This is a standard Bluetooth pairing code (Bonding). It is sent upon request from the BLE stack to establish a secure connection between the ESP32 and the charger.

- **In Code:** `ble_client.passkey_reply` -> `7917` (or `1234`).
- **Where to find it:** 
  - Most commonly **7917** or **1234**.
  - Often identical to the app PIN.

---

## 2. Protocol Authorization PIN (AUTH)

**Usage:**
This is the code sent inside the text command `$BLE,AUTH,XXXX`. Without successful authorization using this code, the charger will not respond to any data queries (`$DATA`) or control commands (`$CMD`).

- **In Code:** `$BLE,AUTH,7917` (sent in the `on_connect` block after 5-8 seconds).
- **Where to find it:**
  - Located on a **sticker on the charger's casing**.
  - Visible in the official **eSolution Charging** app.
  - Common values: **7917**, **9844**, or **001234**.

---

## Operational Logic

1. **Connection**: ESP32 connects to the charger via BLE.
2. **Pairing**: If the charger requires it, ESP32 sends the Passkey. Many models (e.g., eWB11310) use "Just Works" mode and do not require this PIN.
3. **Authorization**: Once connected, ESP32 MUST send `$BLE,AUTH,[PIN]`.
4. **Operation**: After receiving `$BLE,AUTH,OK` from the charger, ESP32 begins periodic data polling.

> [!CAUTION]
> Using the wrong AUTH code usually results in no response (Timeout) or a `$BLE,AUTH,FAIL` error.
