# ESPHome Configuration Repository Setup Guide

This guide explains how to use this repository to manage all your ESPHome device configurations.

## Repository Structure

```
├── devices/            # Your actual device configurations
│   ├── hvac/          # HVAC/Climate control devices
│   ├── sensors/       # Environmental and other sensors  
│   ├── switches/      # Relay controls, smart switches
│   └── other/         # Other device types
├── templates/         # Reusable configuration templates
│   ├── common/        # Base templates (ESP32/ESP8266)
│   ├── hvac/          # HVAC-specific templates
│   └── sensors/       # Sensor-specific templates
├── components/        # Shared component configurations
│   └── connectivity/  # WiFi, OTA, API configurations
└── docs/             # Documentation
```

## Quick Start

### 1. Setting Up Secrets

Before importing any configurations, ensure your ESPHome dashboard has the following secrets configured:

```yaml
# In your ESPHome secrets.yaml file:
wifi_ssid: "YourWiFiName"
wifi_password: "YourWiFiPassword"
api_encryption_key: "your_32_character_api_key_here"
ota_password: "your_ota_password"
ap_password: "fallback_hotspot_password"
```

### 2. Importing Device Configurations

1. Copy any device configuration from the `devices/` directory
2. Import it into your ESPHome dashboard
3. Customize the `substitutions` section for your specific hardware
4. Compile and upload

### 3. Customizing for Your Hardware

Each device configuration uses substitutions for hardware-specific settings:

```yaml
substitutions:
  devicename: "your-device-name"      # Must be unique
  friendly_name: "Your Device Name"   # Display name in HA
  board_type: "esp32dev"              # Your ESP board type
  status_led_pin: "2"                 # LED pin for status
  # ... other device-specific pins
```

## Device Types

### HVAC Devices

Use configurations from `devices/hvac/`:
- `hvac-mastercloset.yaml` - Basic CN105 Mitsubishi control
- `hvac-livingroom-with-dual-setpoint.yaml` - Advanced dual setpoint

**Required substitutions:**
- `uart_tx_pin`, `uart_rx_pin` - CN105 connection pins
- For dual setpoint: `remote_temp_sensor`, `remote_humid_sensor`

### Sensor Nodes

Use configurations from `devices/sensors/`:
- `sensor-livingroom.yaml` - DHT22 temperature/humidity

**Required substitutions:**
- `temp_sensor_pin` - Sensor data pin
- `sensor_update_interval` - How often to read sensors

### Switch Devices

Use configurations from `devices/switches/`:
- `switch-garage.yaml` - Basic relay with button control

**Required substitutions:**
- `relay_pin` - GPIO pin controlling relay
- `button_pin` - Physical button input pin

## Creating New Device Configurations

### 1. Choose a Base Template

Start with the appropriate template from `templates/`:
- `templates/common/base.yaml` - ESP32 devices
- `templates/common/base-esp8266.yaml` - ESP8266 devices
- `templates/hvac/cn105-universal.yaml` - Mitsubishi CN105 devices

### 2. Add Functionality

Include additional templates as needed:
- `templates/sensors/environmental.yaml` - Temperature/humidity
- `templates/sensors/motion.yaml` - PIR motion detection
- `templates/hvac/dual-setpoint-addon.yaml` - Advanced thermostat

### 3. Example New Device

```yaml
# My new sensor node
substitutions:
  devicename: "sensor-bedroom"
  friendly_name: "Bedroom Sensor"
  board_type: "esp32dev"
  status_led_pin: "2"
  temp_sensor_pin: "4"

# Include base functionality
<<: !include ../../templates/common/base.yaml

# Add specific sensors
sensor:
  - platform: dht
    pin: ${temp_sensor_pin}
    temperature:
      name: "${friendly_name} Temperature"
    humidity:
      name: "${friendly_name} Humidity"
    update_interval: 60s
```

## Best Practices

### 1. Naming Conventions
- Use descriptive device names: `hvac-livingroom`, `sensor-kitchen`
- Use consistent friendly names: "Living Room HVAC", "Kitchen Sensor"
- Keep names lowercase with hyphens for device names

### 2. Pin Assignments
- Document pin assignments in comments
- Use substitutions for all pin numbers
- Group related pins together in substitutions

### 3. Secrets Management
- Never commit secrets to this repository
- Use ESPHome's secrets system for all sensitive data
- Test with fake secrets first, then update in ESPHome

### 4. Version Control
- Commit working configurations after testing
- Use meaningful commit messages
- Create branches for experimental changes

## Troubleshooting

### Common Issues

1. **Import Errors**: Check file paths in `!include` statements
2. **Pin Conflicts**: Ensure pins don't conflict with board constraints  
3. **Missing Secrets**: Verify all required secrets are in ESPHome
4. **Template Not Found**: Check relative paths from device config location

### Testing Configurations

1. Start with basic base template
2. Add one feature at a time
3. Test compilation before adding more complexity
4. Use ESPHome's validation features
