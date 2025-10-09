# ESPHome Configuration Repository

![Validate Configs](https://github.com/brianfeucht/esphome-configs/workflows/Validate%20ESPHome%20Configurations/badge.svg)
![CI/CD Pipeline](https://github.com/brianfeucht/esphome-configs/workflows/ESPHome%20CI/CD%20Pipeline/badge.svg)

This repository contains all my ESPHome device configurations as importable packages. **No copy/paste required** - import configurations directly from GitHub using ESPHome's `packages` feature.

All configurations are automatically validated through CI/CD to ensure they compile successfully before merging.

## 🚀 Quick Start

1. **Choose a configuration** from `devices/`
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
├── devices/           # Complete device configs ready for ESPHome import
├── packages/          # Modular packages that can be mixed and matched
├── docs/             # Documentation and setup guides
└── .github/          # CI/CD workflows and automation
```

**Simple and clean** - no duplication, clear purpose for each directory.

## 🎯 Available Configurations

### Ready-to-Import Device Configs
- **`devices/hvac/hvac-mastercloset.yaml`** - Basic CN105 heat pump controller
- **`devices/hvac/hvac-livingroom-with-dual-setpoint.yaml`** - CN105 with dual setpoint thermostat
- **`devices/sensors/sensor-livingroom.yaml`** - DHT22 environmental sensor
- **`devices/switches/switch-garage.yaml`** - Basic relay switch with button

### Modular Packages
- **`packages/base.yaml`** - Essential ESPHome functionality (WiFi, API, OTA, diagnostics)
- **`packages/cn105.yaml`** - Mitsubishi heat pump control via CN105 interface
- **`packages/dual-setpoint.yaml`** - Advanced dual setpoint thermostat (requires cn105)
- **`packages/dht-sensor.yaml`** - DHT22 temperature/humidity sensor
- **`packages/relay-switch.yaml`** - Basic relay control with optional button

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

## 🛠️ Development & CI/CD

This repository includes automated validation to ensure all configurations compile successfully:

- **Automatic Validation**: All device configurations are compiled on every pull request
- **Multiple Workflows**: Simple validation and comprehensive CI/CD pipeline
- **Build Artifacts**: Compiled firmware available for download
- **Documentation Checks**: Markdown links validated automatically

See [`.github/README.md`](.github/README.md) for detailed CI/CD documentation.

## 🤝 Contributing

1. Add your device configuration to the appropriate directory
2. Update the CI/CD matrix to include your new device
3. Create a pull request - validation runs automatically
4. Merge after successful validation
