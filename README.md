# ESPHome Configuration Repository

This repository contains all my ESPHome device configurations as importable packages. **No copy/paste required** - import configurations directly from GitHub using ESPHome's `packages` feature.

## 🚀 Quick Start

1. **Choose a configuration** from `ready-to-import/`
2. **Import directly into ESPHome** - no copying needed!
3. **Customize substitutions** for your hardware
4. **Set secrets** in ESPHome dashboard
5. **Compile and upload**

## 📦 Import Example

```yaml
# In your ESPHome device configuration:
substitutions:
  devicename: "my-hvac"
  friendly_name: "My HVAC"
  board_type: "lolin_s2_mini"
  uart_tx_pin: "39"
  uart_rx_pin: "40"
  status_led_pin: "15"
  climate_update_interval: "1.5s"

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
```

## 📁 Repository Structure

```
├── ready-to-import/     # Complete device configs ready for ESPHome import
├── packages/           # Modular packages that can be mixed and matched
├── devices/           # Legacy device configurations (templates-based)
├── templates/         # Legacy reusable templates  
├── components/        # Legacy shared components
└── docs/             # Documentation
```

## 🎯 Available Packages

### Core Packages
- **`base.yaml`** - Essential ESPHome functionality (WiFi, API, OTA, diagnostics)
- **`cn105.yaml`** - Mitsubishi heat pump control via CN105 interface
- **`dual-setpoint.yaml`** - Advanced dual setpoint thermostat (requires cn105)
- **`dht-sensor.yaml`** - DHT22 temperature/humidity sensor
- **`relay-switch.yaml`** - Basic relay control with optional button

### Ready-to-Import Configurations
- **`hvac-mastercloset.yaml`** - Basic CN105 heat pump controller
- **`hvac-livingroom-dual.yaml`** - CN105 with dual setpoint thermostat
- **`sensor-livingroom.yaml`** - DHT22 environmental sensor
- **`switch-garage.yaml`** - Basic relay switch with button

## 🔧 Customization

All configurations use `substitutions` for hardware-specific settings:

```yaml
substitutions:
  devicename: "unique-device-name"    # Must be unique
  friendly_name: "Display Name"      # Shown in Home Assistant
  board_type: "esp32dev"             # Your ESP board type
  # ... other hardware-specific pins
```

## 🔑 Secrets Management

Configure these secrets in your ESPHome dashboard (never stored in this repo):

```yaml
# ESPHome secrets.yaml
wifi_ssid: "YourWiFiName"
wifi_password: "YourWiFiPassword"  
api_encryption_key: "32-character-key"
ota_password: "your-ota-password"
ap_password: "fallback-password"
```

## 🔄 Workflow

1. **Start with ready-to-import config** or build your own with packages
2. **Import into ESPHome** using the GitHub URL
3. **Customize substitutions** for your specific hardware
4. **Compile and upload** - ESPHome handles the GitHub imports automatically

## 📋 Example Custom Configuration

```yaml
# My custom multi-sensor device
substitutions:
  devicename: "sensor-bedroom"
  friendly_name: "Bedroom Sensor"
  board_type: "esp32dev"
  sensor_pin: "4"
  status_led_pin: "2"
  sensor_update_interval: "60s"

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  dht_sensor: github://brianfeucht/esphome-configs/packages/dht-sensor.yaml

# Add custom sensors or modifications here
sensor:
  - platform: adc
    pin: A0
    name: "${friendly_name} Light Level"
```
