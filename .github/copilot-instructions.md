<!-- Use this file to provide workspace-specific custom instructions to Copilot. For more details, visit https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilotinstructionsmd-file -->

# ESPHome Configuration Repository

This repository contains centralized ESPHome configurations for all my smart home devices, organized with reusable templates and components to minimize code duplication.

## Project Structure
- `devices/` - Individual device configurations ready for ESPHome import
  - `hvac/` - HVAC and climate control devices
  - `sensors/` - Environmental sensors and monitoring devices
  - `switches/` - Relay controllers and smart switches
  - `other/` - Other device types
- `templates/` - Reusable configuration templates
  - `common/` - Base templates for ESP32/ESP8266
  - `hvac/` - HVAC-specific templates (CN105, thermostats)
  - `sensors/` - Sensor-specific templates
- `components/` - Shared component configurations
  - `connectivity/` - WiFi, OTA, API configurations
  - `sensors/` - Sensor component configs
  - `climate/` - Climate component configs
- `docs/` - Documentation and setup guides

## Development Guidelines
- Use YAML best practices for ESPHome configurations
- Maintain compatibility with Home Assistant
- Use modular design with templates and includes
- Test configurations before deployment
- Document all custom parameters and options
- Store secrets in ESPHome dashboard, not in repository
- Use descriptive device naming: `device-type-location`

## Key Features
- **Modular Design**: Reusable templates minimize duplication
- **Multiple Device Types**: HVAC, sensors, switches, and more
- **Centralized Management**: All configs in one place
- **ESPHome Integration**: Import configs directly into dashboard
- **Secret Management**: All secrets handled by ESPHome

## Workflow
1. Copy device config from `devices/` directory
2. Customize substitutions for hardware
3. Import into ESPHome dashboard
4. Set secrets in ESPHome
5. Compile and upload to device

## Progress Tracking
- [x] Verify that the copilot-instructions.md file in the .github directory is created
- [x] Clarify Project Requirements - ESPHome configuration repository for all devices
- [x] Restructure Project - Created organized structure with devices, templates, and components
- [x] Update Templates - Reorganized templates into common and device-specific categories
- [x] Move Device Configurations - Relocated to devices/ directory structure
- [x] Create Base Templates - Built reusable ESP32/ESP8266 base templates
- [x] Update Documentation - Created comprehensive setup guide and device README
- [ ] Install Required Extensions
- [ ] Test Configuration Import
- [ ] Create Additional Device Templates
- [ ] Set Up CI/CD for Validation
