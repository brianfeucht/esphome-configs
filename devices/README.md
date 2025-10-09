# Device Configurations

This directory contains ready-to-use ESPHome device configurations. Each configuration is designed to be imported directly into the ESPHome dashboard.

## Directory Structure

- `hvac/` - Heat pump and climate control devices
- `sensors/` - Environmental sensors and monitoring devices  
- `switches/` - Relay controllers and smart switches
- `other/` - Other device types

## Usage

1. **Copy Configuration**: Choose a device config that matches your hardware
2. **Customize Substitutions**: Update device name, pins, and other hardware-specific settings
3. **Import to ESPHome**: Import the YAML file into your ESPHome dashboard
4. **Set Secrets**: Ensure all required secrets are configured in ESPHome
5. **Compile & Upload**: Build and flash to your device

## Device Naming Convention

Use descriptive names that indicate:
- Device type: `hvac-`, `sensor-`, `switch-`
- Location: `-livingroom`, `-garage`, `-kitchen`
- Purpose: `-mastercloset`, `-dual` (for special variants)

Examples:
- `hvac-livingroom.yaml`
- `sensor-kitchen.yaml` 
- `switch-garage.yaml`

## Customization

Each device config uses substitutions for easy customization:

```yaml
substitutions:
  devicename: "unique-device-name"    # Must be unique across all devices
  friendly_name: "Display Name"      # Shown in Home Assistant
  board_type: "esp32dev"             # Your ESP32/ESP8266 board
  # ... hardware-specific pins and settings
```

## Testing

Before deploying to production:
1. Validate configuration: Check for syntax errors
2. Test compilation: Ensure it builds successfully
3. Test upload: Flash to test device first
4. Verify functionality: Test all features work as expected

## Templates Used

Device configurations reference templates from `../templates/`:
- `common/base.yaml` - Core ESPHome functionality
- `hvac/cn105-universal.yaml` - Mitsubishi heat pump control
- `sensors/environmental.yaml` - Temperature/humidity sensors
- And more...

Modify template references if you move configurations to different locations.