# ESPHome Packages

This directory contains modular ESPHome packages that can be imported individually or combined to create custom device configurations.

## 📦 Available Packages

### Core Package

#### `base.yaml`
Essential ESPHome functionality required by all devices
- ESP32/ESP8266 configuration
- WiFi, API, OTA setup
- Basic diagnostics (uptime, WiFi signal, version info)
- Status LED support
- Time synchronization

**Import with:**
```yaml
packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
```

### Device-Specific Packages

#### `cn105.yaml`
Mitsubishi heat pump control via CN105 interface
- External component for CN105
- UART configuration
- Climate entity with full heat pump control
- Vane controls and diagnostic sensors

**Import with:**
```yaml
packages:
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
```

**Required substitutions:**
- `uart_tx_pin` - CN105 TX connection pin
- `uart_rx_pin` - CN105 RX connection pin
- `climate_update_interval` - Update frequency

#### `dual-setpoint.yaml`
Advanced dual setpoint thermostat functionality
- Meta thermostat platform
- Heating/cooling deadbands and overrun protection
- Multiple presets (Home, Away, Sleep)
- Temperature limits and timing controls

**Import with:**
```yaml
packages:
  dual_setpoint: github://brianfeucht/esphome-configs/packages/dual-setpoint.yaml
```

**Dependencies:** Requires `cn105.yaml` package

#### `remote-temperature.yaml`
Home Assistant remote temperature sensor integration
- Uses external HA sensor instead of heat pump's built-in sensor
- Temperature validation and filtering
- Automatic fallback to built-in sensor on timeout
- Unit conversion support (F to C)

**Import with:**
```yaml
packages:
  remote_temp: github://brianfeucht/esphome-configs/packages/hvac/remote-temperature.yaml
```

**Required substitutions:**
- `remote_temp_sensor` - Home Assistant sensor entity_id (e.g., `sensor.room_temperature`)

**Dependencies:** Requires `cn105.yaml` package

See [Remote Temperature Documentation](../docs/remote-temperature.md) for details.

#### Coming Soon
- `dht-sensor.yaml` - DHT22 temperature and humidity sensor
- `relay-switch.yaml` - Basic relay control with optional physical button

## 🔧 Using Packages

### Single Package
```yaml
substitutions:
  devicename: "my-hvac"
  friendly_name: "My HVAC"
  # ... hardware-specific substitutions

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
```

### Multiple Packages
```yaml
substitutions:
  devicename: "my-hvac"
  friendly_name: "My HVAC"
  # ... hardware-specific substitutions

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
  dual_setpoint: github://brianfeucht/esphome-configs/packages/dual-setpoint.yaml
```

### With Custom Additions
```yaml
substitutions:
  # ... your substitutions

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  # Add additional packages when available

# Add your custom components
sensor:
  - platform: adc
    pin: A0
    name: "${friendly_name} Light Level"
    
switch:
  - platform: gpio
    pin: 12
    name: "${friendly_name} Custom Output"
```

## 📋 Common Substitutions

Most packages expect these common substitutions:

```yaml
substitutions:
  # Device identity
  devicename: "unique-device-name"      # Must be unique
  friendly_name: "Display Name"        # Shown in Home Assistant
  
  # Hardware
  board_type: "esp32dev"               # ESP32/ESP8266 board type
  status_led_pin: "2"                  # Status LED pin (optional)
```

## 🔄 Package Dependencies

Some packages depend on others:
- **`dual-setpoint.yaml`** requires **`cn105.yaml`**
- Most configurations should include **`base.yaml`**

Dependencies are not automatically resolved - you must import all required packages.

## 🛠️ Creating Custom Packages

To create your own packages:

1. **Create a new YAML file** in this directory
2. **Add package documentation** at the top as comments
3. **Use substitutions** for configurable values
4. **Test with a device configuration**
5. **Document any dependencies**

Example template:
```yaml
# My Custom Package
# Import with: packages:
#   my_package: github://brianfeucht/esphome-configs/packages/my-package.yaml

# Package components here
sensor:
  - platform: template
    name: "${friendly_name} Custom Sensor"
    # ... configuration
```