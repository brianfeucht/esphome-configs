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
