# Ready-to-Import ESPHome Configurations

These configurations can be imported directly into ESPHome with **no copy/paste required**. Each file imports the necessary packages from this GitHub repository automatically.

## 🚀 How to Use

1. **Copy the configuration URL** from GitHub (raw file link)
2. **Paste into ESPHome dashboard** as a new device  
3. **Customize substitutions** for your hardware
4. **Compile and upload**

## 📋 Available Configurations

### HVAC Controllers

#### `hvac-mastercloset.yaml`
Basic Mitsubishi CN105 heat pump controller
- **Packages**: base + cn105
- **Hardware**: Lolin S2 Mini (configurable)
- **Features**: Basic heat pump control, diagnostics

#### `hvac-livingroom-dual.yaml`  
Advanced CN105 with dual setpoint thermostat
- **Packages**: base + cn105 + dual-setpoint
- **Hardware**: Lolin S2 Mini (configurable)
- **Features**: Dual setpoint control, presets, advanced scheduling

### Sensor Nodes

#### `sensor-livingroom.yaml`
DHT22 temperature and humidity sensor
- **Packages**: base + dht-sensor
- **Hardware**: Any ESP32/ESP8266
- **Features**: Temperature, humidity, diagnostics

### Switch Controllers

#### `switch-garage.yaml`
Basic relay switch with physical button
- **Packages**: base + relay-switch
- **Hardware**: Any ESP32/ESP8266
- **Features**: Relay control, button toggle, diagnostics

## ⚙️ Customization

Each configuration uses substitutions for easy customization:

```yaml
substitutions:
  # Device identity (must be unique)
  devicename: "your-device-name"
  friendly_name: "Your Device Name"
  
  # Hardware configuration
  board_type: "esp32dev"        # Your ESP board
  status_led_pin: "2"           # Status LED pin
  
  # Device-specific pins and settings
  # ... see individual configs for options
```

## 🔧 Creating Custom Configurations

You can also create your own configurations by mixing packages:

```yaml
# Custom configuration example
substitutions:
  devicename: "my-custom-device"
  friendly_name: "My Custom Device"
  board_type: "esp32dev"
  # ... other substitutions

packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  dht_sensor: github://brianfeucht/esphome-configs/packages/dht-sensor.yaml
  # Add more packages as needed

# Add custom components here
sensor:
  - platform: adc
    pin: A0
    name: "${friendly_name} Custom Sensor"
```

## 📦 Package Dependencies

Some packages require others to be imported first:

- **`dual-setpoint.yaml`** requires **`cn105.yaml`**
- All configurations should include **`base.yaml`**

The ready-to-import configs handle these dependencies automatically.

## 🔑 Required Secrets

Make sure these are configured in your ESPHome secrets before compiling:

```yaml
wifi_ssid: "YourWiFiNetwork"
wifi_password: "YourWiFiPassword"
api_encryption_key: "32-character-encryption-key"
ota_password: "your-ota-password"
ap_password: "fallback-hotspot-password"
```

## 🐛 Troubleshooting

### Import Issues
- Ensure GitHub repository is public
- Check internet connection during compilation
- Verify file paths in package imports

### Compilation Errors
- Check substitution values match your hardware
- Verify all required secrets are configured
- Review pin assignments for conflicts

### Hardware Issues
- Verify pin assignments match your board
- Check power supply and connections
- Test with minimal configuration first