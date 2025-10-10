# Continuous Integration & Deployment

This directory contains GitHub Actions workflows that automatically validate ESPHome configurations using ESPHome's official build action.

## Workflow

### `ci-cd.yml` - ESPHome CI/CD Build & Validate
A consolidated workflow that builds all device configurations to ensure they compile successfully.

**Triggers:**
- Push to `main` branch
- Pull requests to `main` branch  
- Manual dispatch

**Features:**
- **ESPHome Official Action**: Uses `esphome/build-action@v3.1.0`
- **Parallel Builds**: Compiles all device configs simultaneously  
- **Descriptive Names**: Clear job names for each device type
- **Stable Version**: Always uses the latest stable ESPHome release
- **GitHub Package Support**: Validates configurations that import packages from GitHub

## Device Configuration Matrix

The workflow automatically tests these device configurations:

| Device Type | Configuration File | Description |
|-------------|-------------------|-------------|
| HVAC | `devices/hvac/hvac-livingroom-with-dual-setpoint.yaml` | Living room HVAC with dual setpoint control |
| HVAC | `devices/hvac/hvac-mastercloset.yaml` | Master closet HVAC unit |

## Adding New Devices

To add a new device to the validation pipeline, update the matrix in the workflow file:

```yaml
strategy:
  matrix:
    include:
      - name: "HVAC Living Room Dual Setpoint"
        yaml_file: devices/hvac/hvac-livingroom-with-dual-setpoint.yaml
      - name: "HVAC Master Closet"
        yaml_file: devices/hvac/hvac-mastercloset.yaml
      - name: "Your New Device"                    # Add descriptive name
        yaml_file: devices/category/your-device.yaml  # Add file path
```

## ESPHome Build Action

We use ESPHome's official GitHub action which provides:

- **Automatic ESPHome Installation**: No manual setup required
- **Version Management**: Uses stable ESPHome releases
- **Platform Support**: Supports ESP32, ESP8266, and other platforms
- **Error Reporting**: Clear build failure messages
- **Caching**: Optimized build times through intelligent caching

## Status Badges

Add this to your README to show build status:

```markdown
![ESPHome CI/CD](https://github.com/brianfeucht/esphome-configs/workflows/ESPHome%20CI%2FCD%20-%20Build%20%26%20Validate/badge.svg)
```

## Troubleshooting

### Common Issues

1. **Build Failures**: 
   - Check that all package imports are correct (GitHub URLs)
   - Verify substitutions are properly defined
   - Ensure platform compatibility (ESP32 vs ESP8266)

2. **Missing Dependencies**:
   - Check that all referenced packages exist in the repository
   - Verify component availability in ESPHome version
   - Ensure packages have correct dependencies (e.g., dual-setpoint requires cn105)

3. **Action Failures**:
   - Check the action logs for specific error messages
   - Ensure YAML syntax is valid
   - Verify GitHub repository is public for package imports

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