# Continuous Integration & Deployment

This directory contains GitHub Actions workflows that automatically validate ESPHome configurations using ESPHome's official build action.

## Workflows

### 1. `validate-configs.yml` - Simple Validation
A basic workflow that builds all device configurations to ensure they compile successfully.

**Triggers:**
- Push to `main` branch
- Pull requests to `main` branch  
- Manual dispatch

**What it does:**
- Uses ESPHome's official `esphome/build-action` to validate and compile configurations
- Tests each device configuration with the stable ESPHome version
- Reports success/failure status

### 2. `ci-cd.yml` - Enhanced Build Pipeline  
An enhanced version with descriptive names and organized matrix.

**Triggers:**
- Push to `main` branch
- Pull requests to `main` branch
- Manual dispatch

**Features:**
- **ESPHome Official Action**: Uses `esphome/build-action@v3.1.0`
- **Parallel Builds**: Compiles all device configs simultaneously  
- **Descriptive Names**: Clear job names for each device type
- **Stable Version**: Always uses the latest stable ESPHome release

## Device Configuration Matrix

The workflows automatically test these device configurations:

| Device Type | Configuration File | Description |
|-------------|-------------------|-------------|
| HVAC | `devices/hvac/hvac-livingroom-with-dual-setpoint.yaml` | Living room HVAC with dual setpoint control |
| HVAC | `devices/hvac/hvac-mastercloset.yaml` | Master closet HVAC unit |
| Sensor | `devices/sensors/sensor-livingroom.yaml` | Environmental sensor for living room |
| Switch | `devices/switches/switch-garage.yaml` | Garage door/light switch controller |

## Adding New Devices

To add a new device to the validation pipeline, update the matrix in both workflow files:

```yaml
strategy:
  matrix:
    yaml_file:  # or include: for enhanced pipeline
      - devices/hvac/hvac-livingroom-with-dual-setpoint.yaml
      - devices/hvac/hvac-mastercloset.yaml  
      - devices/sensors/sensor-livingroom.yaml
      - devices/switches/switch-garage.yaml
      - devices/your-category/your-new-device.yaml  # Add here
```

## ESPHome Build Action

We use ESPHome's official GitHub action which provides:

- **Automatic ESPHome Installation**: No manual setup required
- **Version Management**: Uses stable ESPHome releases
- **Platform Support**: Supports ESP32, ESP8266, and other platforms
- **Error Reporting**: Clear build failure messages
- **Caching**: Optimized build times through intelligent caching

## Status Badges

Add these to your README to show build status:

```markdown
![Validate Configs](https://github.com/brianfeucht/esphome-configs/workflows/Validate%20ESPHome%20Configurations/badge.svg)
![ESPHome Build](https://github.com/brianfeucht/esphome-configs/workflows/ESPHome%20Build%20%26%20Validate/badge.svg)
```

## Troubleshooting

### Common Issues

1. **Build Failures**: 
   - Check that all `!include` paths are correct
   - Verify substitutions are properly defined
   - Ensure platform compatibility (ESP32 vs ESP8266)

2. **Missing Dependencies**:
   - Check that all referenced templates exist
   - Verify component availability in ESPHome version

3. **Action Failures**:
   - Check the action logs for specific error messages
   - Ensure YAML syntax is valid

### Local Testing

Test your configurations locally before pushing:

```bash
# Install ESPHome  
pip install esphome

# Validate configuration
esphome config devices/your-device.yaml

# Compile (without upload)
esphome compile devices/your-device.yaml
```

## ESPHome Action Reference

The workflows use the official ESPHome build action:

```yaml
- name: Build ESPHome configuration
  uses: esphome/build-action@v3.1.0
  with:
    yaml_file: path/to/config.yaml
    version: stable  # or specific version like "2024.9.2"
```

For more information, see the [ESPHome Build Action](https://github.com/esphome/build-action) repository.