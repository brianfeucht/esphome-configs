# Dual Setpoint Configuration Guide

The dual setpoint functionality provides advanced thermostat control with separate heating and cooling setpoints, similar to traditional HVAC thermostats.

## How It Works

The dual setpoint system uses ESPHome's `thermostat` platform to create a meta-thermostat that controls your CN105 heat pump. It monitors remote temperature sensors and automatically switches between heating, cooling, and idle modes based on your setpoints.

## Key Components

### 1. Meta Thermostat
- Controls the CN105 climate device
- Provides separate heating/cooling setpoints
- Manages presets (Home, Away, Sleep)
- Handles deadbands and overrun protection

### 2. Remote Sensors
- Temperature sensor (required)
- Humidity sensor (optional)
- Must be entities from Home Assistant

### 3. CN105 Climate Device
- Physical interface to heat pump
- Controlled by meta thermostat
- Provides vane controls and diagnostics

## Configuration

### Temperature Sensors

Set up sensors in your substitutions:

```yaml
substitutions:
  remote_temp_sensor: "sensor.living_room_temperature"
```

These must be existing entities in Home Assistant.

### Presets

The configuration includes three presets:

- **Home**: Normal comfort settings (21-24°C)
- **Away**: Energy saving (16-26°C) 
- **Sleep**: Night comfort (19-25°C)

Customize in `components/climate/meta_thermostat.yaml`:

```yaml
preset:
  - name: Home
    default_target_temperature_low: 21 °C
    default_target_temperature_high: 24 °C
```

### Deadbands and Timing

Configure deadbands to prevent short cycling:

```yaml
heat_deadband: 0.5 °C    # Temperature below setpoint before heating
cool_deadband: 0.5 °C    # Temperature above setpoint before cooling
heat_overrun: 0.5 °C     # Continue heating until this above setpoint
cool_overrun: 0.5 °C     # Continue cooling until this below setpoint
```

Minimum run/off times prevent equipment damage:

```yaml
min_cooling_off_time: 300s   # 5 minutes between cooling cycles
min_cooling_run_time: 300s   # Minimum cooling runtime
min_heating_off_time: 300s   # 5 minutes between heating cycles  
min_heating_run_time: 300s   # Minimum heating runtime
```

## Usage

### In Home Assistant

You'll see two climate entities:

1. **Heat Pump**: Direct CN105 control (usually hidden)
2. **Thermostat**: Main dual setpoint control

Use the Thermostat entity for daily control.

### Setting Temperatures

- **Heating setpoint**: Lower temperature
- **Cooling setpoint**: Upper temperature
- **Dead zone**: Between setpoints (no heating/cooling)

Example:
- Heat to 21°C, Cool to 24°C
- Room at 22°C: No action (in dead zone)
- Room at 20°C: Start heating
- Room at 25°C: Start cooling

### Automation Examples

**Schedule-based presets:**
```yaml
automation:
  - alias: "Set Away Mode"
    trigger:
      platform: time
      at: "08:00:00"
    action:
      service: climate.set_preset_mode
      target:
        entity_id: climate.living_room_thermostat
      data:
        preset_mode: "Away"
```

**Presence-based control:**
```yaml
automation:
  - alias: "Home Mode When Present"
    trigger:
      platform: state
      entity_id: person.john
      to: "home"
    action:
      service: climate.set_preset_mode
      target:
        entity_id: climate.living_room_thermostat
      data:
        preset_mode: "Home"
```

## Advanced Configuration

### Custom Actions

Add custom actions for different modes:

```yaml
heat_action:
  - climate.control:
      id: hp
      mode: HEAT
  - light.turn_on:  # Visual indicator
      id: heating_led

cool_action:
  - climate.control:
      id: hp  
      mode: COOL
  - light.turn_on:  # Visual indicator
      id: cooling_led
```

### Multiple Zones

For multi-zone setups, create separate meta thermostats:

```yaml
climate:
  - !include components/climate/cn105_climate.yaml
  - !include components/climate/zone1_thermostat.yaml  
  - !include components/climate/zone2_thermostat.yaml
```

## Troubleshooting

### Common Issues

1. **Thermostat not responding:**
   - Check remote sensor entity IDs
   - Verify sensors are updating in HA
   - Check deadband settings

2. **Short cycling:**
   - Increase minimum run/off times
   - Adjust deadbands
   - Check sensor placement

3. **Temperature overshoot:**
   - Reduce overrun values
   - Increase deadbands
   - Check heat pump response time

### Monitoring

Key entities to monitor:

- `sensor.thermostat_action`: Current action (heating/cooling/idle)
- `climate.heat_pump`: Direct heat pump status
- Remote temperature/humidity sensors

Check logs for thermostat decisions:
```
[climate.thermostat] Switching to HEATING mode
[climate.thermostat] Temperature 20.5°C below heating setpoint 21.0°C
```
