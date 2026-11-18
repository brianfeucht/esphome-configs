# ESPHome Configuration Repository

This repository contains my ESPHome device configurations as importable packages.  This allows me to keep my configs in source control vs just stored in my EspHome install.

EspHome requires these be public to import.  All of the configs here are unique to my builds.  They might be okay reference material but are generally useless to you without hardware designs.  I'm not documenting my hardware as most of this is "as-built"

If you have found this repo and find it useful, good for you.  Otherwise I am not supporting any of this.

## 📦 Import Example

```yaml
# In your ESPHome device configuration:
substitutions:
  devicename: "hvac-office"

packages:
  esphome-configs:
    url: https://github.com/brianfeucht/esphome-configs
    files: [packages/base.yaml, packages/cn105.yaml]
    ref: main
```

## 📁 Repository Structure

```
├── devices/           # Complete device configs ready for ESPHome import
├── packages/          # Modular packages that can be mixed and matched
├── docs/             # Documentation and setup guides
└── .github/          # CI/CD workflows and automation
```

## 🎯 Available Configurations

### Modular Packages
- **`packages/base.yaml`** - Essential ESPHome functionality (WiFi, API, OTA, diagnostics)
- **`packages/hvac/cn105.yaml`** - Mitsubishi heat pump control via CN105 interface
- **`packages/hvac/dual-setpoint.yaml`** - Advanced dual setpoint thermostat (requires cn105)
- **`packages/hottub/balboa.yaml`** - Balboa Spa control
- **`packages/display/cyd-2432s028r.yaml`** - ESP32-2432S028R "Cheap Yellow Display" hardware (portrait LVGL, touch, backlight dimming)
- **`packages/display/west-office-panel.yaml`** - West Office wall panel UI: lights, shades, HVAC, CO2 (requires cyd-2432s028r)
- **`packages/garage/ratgdo-drycontact-enc.yaml`** - ratgdo32 v3.2 garage door opener, dry contact + encoder (Leavenworth)
- **`packages/audio/hifi-esp32-s3.yaml`** - Sonocotta HiFi-ESP32-S3 Sendspin player (Leavenworth)
- **`packages/audio/louder-plus-s3.yaml`** - Sonocotta Louder-ESP32-S3-Plus amp for a passive speaker (Leavenworth)
- **`packages/propane/propane-monitor.yaml`** - Propane tank level from the tank sensor's BLE advertisements (Leavenworth)
- **`packages/display/crowpanel-p4-101.yaml`** - Elecrow CrowPanel Advanced 10.1" ESP32-P4 hardware (MIPI-DSI panel, touch, backlight, C6 Wi-Fi)
- **`packages/display/main-panel/`** - Leavenworth main room wall panel UI, one package per area (requires crowpanel-p4-101)
