# ESPHome Configuration Repository

![ESPHome CI/CD](https://github.com/brianfeucht/esphome-configs/workflows/ESPHome%20CI%2FCD%20-%20Build%20%26%20Validate/badge.svg)

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

**Simple and clean** - no duplication, clear purpose for each directory.

## 🎯 Available Configurations

### Modular Packages
- **`packages/base.yaml`** - Essential ESPHome functionality (WiFi, API, OTA, diagnostics)
- **`packages/hvac/cn105.yaml`** - Mitsubishi heat pump control via CN105 interface
- **`packages/hvac/dual-setpoint.yaml`** - Advanced dual setpoint thermostat (requires cn105)


## 🔄 Workflow

1. **Start with ready-to-import config** or build your own with packages
2. **Import into ESPHome** using the GitHub URL
3. **Customize substitutions** for your specific hardware
4. **Compile and upload** - ESPHome handles the GitHub imports automatically

## 📋 Example Custom Configuration

```yaml
# My custom HVAC device
substitutions:
  devicename: "hvac-bedroom"

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  cn105: github://brianfeucht/esphome-configs/packages/hvac/cn105.yaml

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
