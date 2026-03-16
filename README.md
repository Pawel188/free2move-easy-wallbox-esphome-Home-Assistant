# Easy Wallbox ESPHome Integration

ESHome-based integration for eSolution Charging Easy Wallbox using BLE.

## Overview

This project allows for remote monitoring and control of the Easy Wallbox charger without the need for the official mobile app. All BLE communication logic is implemented directly within ESPHome for stability and performance.

### Key Features

- **Energy Monitoring**: Real-time reading of Voltage (V), Current (A), Power (kW), and Session Energy (kWh).
- **Charging Control**: Start/Stop charging switch.
- **Power Management**: Set Current Limits (User Limit and DPM Limit) in kW.
- **DPM Status**: Dynamic Power Management toggle.
- **Native Integration**: Full compatibility with Home Assistant via the ESPHome native API.

## PIN Codes

Important: The charger utilizes two levels of security (BLE Passkey and AUTH Command). See [PIN_GUIDE.md](./PIN_GUIDE.md) for detailed information.

## Installation

1. Copy `easywallbox-proxy.yaml` and `secrets.yaml.example` to your ESPHome configuration directory.
2. Rename `secrets.yaml.example` to `secrets.yaml` and fill in your credentials (WiFi, API keys).
3. **Set your PIN** in the YAML file (within `on_connect` and `on_passkey_request` sections). The default is set to `7917`.
4. Compile and flash the firmware to your ESP32 device (ESP32-S3 recommended).
5. Add the device to Home Assistant.

## Documentation

- [PIN Code System Guide](./PIN_GUIDE.md)
- [Future Documentation Plan](./DOCS_PLAN.md)

---
This project is based on reverse-engineering the charger's Bluetooth protocol.
