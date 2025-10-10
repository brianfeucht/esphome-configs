<!-- Use this file to provide workspace-specific custom instructions to Copilot. For more details, visit https://code.visualstudio.com/docs/copilot/copilot-customization#_use-a-githubcopilotinstructionsmd-file -->

# ESPHome Configuration Repository

This repository contains centralized ESPHome configurations for all my smart home devices, organized with reusable templates and components to minimize code duplication.

## Project Structure
- `test-configs/` - Complete device configurations ready for ESPHome validation and testing
- `packages/` - Modular ESPHome packages for building custom configurations
- `docs/` - Documentation and setup guides

## Development Guidelines
- Use YAML best practices for ESPHome configurations
- Maintain compatibility with Home Assistant
- Use modular design with GitHub package imports (no local includes)
- **ALWAYS test configurations before deployment**
- **Run full build tests before committing changes**
- Document all custom parameters and options
- Store secrets in ESPHome dashboard, not in repository
- Use descriptive device naming: `device-type-location`
- Validate syntax with `esphome config test-configs/hvac-local.yaml`
- Test compilation with `esphome compile test-configs/hvac-local.yaml`

## Key Features
- **Modular Design**: Reusable packages minimize duplication
- **Multiple Device Types**: HVAC, sensors, switches, and more
- **Centralized Management**: All configs in one place
- **ESPHome Integration**: Import configs directly into dashboard
- **Secret Management**: All secrets handled by ESPHome
- **GitHub Package Imports**: No local file dependencies

## Testing & Validation

### Quick Configuration Test
Before making changes, always validate configurations:
```bash
# Navigate to test-configs directory
cd test-configs

# Test configuration syntax and compilation
esphome config hvac-local.yaml
```

### Full Build Test
For comprehensive validation (includes actual firmware compilation):
```bash
# Navigate to test-configs directory  
cd test-configs

# Run full compilation test (takes 2-5 minutes first time)
esphome compile hvac-local.yaml
```

### Copilot Session Testing
When working with GitHub Copilot:

1. **Navigation**: Always use `cd test-configs` to get to test directory
2. **Terminal Persistence**: Use same terminal session to avoid path issues
3. **Path Validation**: Copilot should verify current directory before running commands
4. **Monitoring Builds**: For long compilations, use background mode and poll:
   ```bash
   # Start background compilation in correct directory
   cd test-configs && esphome compile hvac-local.yaml
   
   # Monitor progress by polling terminal output
   # (Copilot will poll terminal status automatically)
   ```
5. **Test File**: Always use `test-configs/hvac-local.yaml` for validation
6. **Secrets**: Test secrets are in `test-configs/secrets.yaml`
7. **Terminal Issues**: If terminal changes directories unexpectedly, always navigate back to `test-configs`
8. **Compilation Status**: Background compilations can be monitored by checking terminal output periodically

### Development Workflow
Always test configurations before committing:

1. **Before Changes**: Run `esphome config hvac-local.yaml` to validate current state
2. **During Development**: Test changes incrementally with config validation
3. **After Changes**: Run full compilation test `esphome compile hvac-local.yaml`
4. **Before Commit**: Ensure all tests pass - **NO COMMITS WITHOUT SUCCESSFUL BUILD**
5. **Pull Request**: Include test results in PR description
6. **Merge Criteria**: Successful compilation required for merge approval

**Required Tests for All Changes:**
- ✅ Configuration syntax validation (`esphome config`)
- ✅ Full firmware compilation (`esphome compile`) 
- ✅ No compilation errors or warnings
- ✅ Memory usage within acceptable limits

### Test Environment
- **Test Config**: `test-configs/hvac-local.yaml` (uses local package imports)
- **Secrets**: `test-configs/secrets.yaml` (test credentials only)
- **Build Output**: `test-configs/.esphome/build/` (gitignored)
- **Expected Time**: Config validation ~10s, Full build ~2-5min (first time)

### Testing Troubleshooting

**Common Issues:**
1. **Directory Path Problems**: Always verify you're in `test-configs` directory
2. **File Not Found**: Check that you're using `hvac-local.yaml` (not the old filenames)
3. **Secrets Missing**: Ensure `secrets.yaml` exists with proper base64 encryption key
4. **Permission Issues**: Run PowerShell as regular user (not admin)
5. **Build Interruption**: If build is cancelled, clean with `esphome clean hvac-local.yaml`

**Build Status Monitoring:**
```bash
# Check if compilation is still running
Get-Process | Where-Object {$_.ProcessName -like "*esphome*"}

# Clean build cache if needed
esphome clean hvac-local.yaml
```

## Workflow
1. Choose device config from `devices/` directory
2. **TEST**: Validate with `esphome config test-configs/hvac-local.yaml`
3. Import directly into ESPHome dashboard using GitHub URL
4. Customize substitutions for hardware
5. Set secrets in ESPHome
6. **TEST**: Run build test before deployment
7. Compile and upload to device
