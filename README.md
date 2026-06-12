# Easy Wallbox ESPHome Integration

ESPHome-based integration for eSolution Charging Easy Wallbox using BLE.

> [!NOTE]
> This project is actively under development. We have reverse-engineered the BLE protocol to provide full remote monitoring, limit control, and state synchronization.

## Overview

This project allows for remote monitoring and control of the Easy Wallbox charger without the need for the official mobile app. All BLE communication logic is implemented directly within ESPHome for stability and performance.

### Key Features

- **Energy Monitoring**: Real-time reading of Voltage (V), Current (A), Power (kW), and Session Energy (kWh).
- **Physical Connection Sensor**: Real-time detection of whether the charging cable is physically plugged into the car (using CP line voltage parsing).
- **Automatic State Synchronization**: The charging switch in Home Assistant automatically synchronizes with the charger's state. When the car is unplugged, the charging switch automatically resets to `ON` (Armed), preparing it for the next session.
- **Dedicated Charging Control**: Start/Stop charging switch with automated DPM control (DPM is disabled on start to ensure charging doesn't get blocked at 0.0 A when a physical meter is absent).
- **Power Management Sliders**: Set User Limit and DPM Limit in kW (range: 1.38 kW to 7.4 kW, minimum 6 A). Sliders only update the respective EEPROM limits and do not trigger unexpected charging states.
- **Secrets Management**: Clean structure separating sensitive credentials (Wi-Fi, API keys) into `secrets.yaml`.
- **Performance Optimized**: Logging level set to `WARN` to minimize CPU/BLE overhead and clean up log output.

## PIN Codes

Important: The charger utilizes two levels of security (BLE Passkey and AUTH Command). See [PIN_GUIDE.md](./PIN_GUIDE.md) for detailed information.

## Installation

1. Copy `easywallbox-proxy.yaml` and `secrets.yaml.example` to your ESPHome configuration directory.
2. Rename `secrets.yaml.example` to `secrets.yaml` and fill in your credentials (WiFi SSID/password, API keys).
3. **Set your PIN** in the YAML file (within `on_connect` and `on_passkey_request` sections). The default is set to `7917`.
4. Compile and flash the firmware to your ESP32 device (ESP32-S3 recommended).
5. Add the device to Home Assistant.

## Documentation

- [PIN Code System Guide](./PIN_GUIDE.md)
- [Future Documentation Plan](./DOCS_PLAN.md)
- [Summary of Session Work (Polish)](./podsumowanie_prac.md)

---
This project is based on reverse-engineering the charger's Bluetooth protocol.
