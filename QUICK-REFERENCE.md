# Quick Reference - ESPHome Package Imports

Copy these import statements into your ESPHome device configurations:

## 📦 Individual Packages

### Base Package (Required for all devices)
```yaml
packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
```

### CN105 Mitsubishi Heat Pump
```yaml
packages:
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
```

### Dual Setpoint Thermostat (requires CN105)
```yaml
packages:
  dual_setpoint: github://brianfeucht/esphome-configs/packages/dual-setpoint.yaml
```

### DHT Temperature/Humidity Sensor
```yaml
packages:
  dht_sensor: github://brianfeucht/esphome-configs/packages/dht-sensor.yaml
```

### Relay Switch with Button
```yaml
packages:
  relay_switch: github://brianfeucht/esphome-configs/packages/relay-switch.yaml
```

## 🎯 Common Combinations

### Basic HVAC Controller
```yaml
packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
```

### Advanced HVAC with Dual Setpoint
```yaml
packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  cn105: github://brianfeucht/esphome-configs/packages/cn105.yaml
  dual_setpoint: github://brianfeucht/esphome-configs/packages/dual-setpoint.yaml
```

### Environmental Sensor
```yaml
packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  dht_sensor: github://brianfeucht/esphome-configs/packages/dht-sensor.yaml
```

### Smart Switch
```yaml
packages:
  esphome_base: github://brianfeucht/esphome-configs/packages/base.yaml
  relay_switch: github://brianfeucht/esphome-configs/packages/relay-switch.yaml
```

## 🚀 Ready-to-Import URLs

For ESPHome dashboard direct import:

- **HVAC Master Closet**: `https://raw.githubusercontent.com/brianfeucht/esphome-configs/main/ready-to-import/hvac-mastercloset.yaml`
- **HVAC Living Room Dual**: `https://raw.githubusercontent.com/brianfeucht/esphome-configs/main/ready-to-import/hvac-livingroom-dual.yaml`
- **Living Room Sensor**: `https://raw.githubusercontent.com/brianfeucht/esphome-configs/main/ready-to-import/sensor-livingroom.yaml`
- **Garage Switch**: `https://raw.githubusercontent.com/brianfeucht/esphome-configs/main/ready-to-import/switch-garage.yaml`