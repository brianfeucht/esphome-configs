<!-- Use this file to provide workspace-specific custom instructions to Copilot. For more details, visit https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilotinstructionsmd-file -->

# ESPHome Configuration Repository

This repository contains centralized ESPHome configurations for all my smart home devices, organized with reusable templates and components to minimize code duplication.

## Project Structure
- `devices/` - Complete device configurations ready for ESPHome import
  - `hvac/` - HVAC and climate control devices
  - `sensors/` - Environmental sensors and monitoring devices
  - `switches/` - Relay controllers and smart switches
  - `other/` - Other device types
- `packages/` - Modular ESPHome packages for building custom configurations
- `docs/` - Documentation and setup guides

## Development Guidelines
- Use YAML best practices for ESPHome configurations
- Maintain compatibility with Home Assistant
- Use modular design with GitHub package imports (no local includes)
- Test configurations before deployment
- Document all custom parameters and options
- Store secrets in ESPHome dashboard, not in repository
- Use descriptive device naming: `device-type-location`

## Key Features
- **Modular Design**: Reusable packages minimize duplication
- **Multiple Device Types**: HVAC, sensors, switches, and more
- **Centralized Management**: All configs in one place
- **ESPHome Integration**: Import configs directly into dashboard
- **Secret Management**: All secrets handled by ESPHome
- **GitHub Package Imports**: No local file dependencies

## Workflow
1. Choose device config from `devices/` directory
2. Import directly into ESPHome dashboard using GitHub URL
3. Customize substitutions for hardware
4. Set secrets in ESPHome
5. Compile and upload to device

## Progress Tracking
- [x] Verify that the copilot-instructions.md file in the .github directory is created
- [x] Clarify Project Requirements - ESPHome configuration repository for all devices
- [x] Restructure Project - Clean, simple structure with no duplication
- [x] Standardize on GitHub Package Imports - All configs use packages approach
- [x] Move Device Configurations - All ready-to-import configs in devices/ directory
- [x] Create Modular Packages - Built reusable packages for common functionality
- [x] Update Documentation - Updated all README files for new structure
- [x] Remove Duplicate Directories - Eliminated templates/, components/, ready-to-import/
- [x] Consolidate CI/CD Workflows - Combined duplicate workflows into single ci-cd.yml
- [ ] Complete Missing Package Files - Add remaining package implementations
- [ ] Test Configuration Import - Verify GitHub package imports work correctly
- [ ] Install Required Extensions - Set up development environment
