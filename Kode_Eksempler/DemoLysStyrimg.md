# Demo Lysstyring med SNZB-01 & SNZB-03

## Lovelace Demo Lysstyring

![](./Images/Demo_Lysstyring_2022-10-22_17-53-09.png)

### Lovelace Demo Lysstyring Edit in visual editor

![Demo_Lysstyring_Love_2022-10-22_17-54-54.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-54-54.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-03.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-03.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-11.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-11.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-17.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-17.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-24.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-24.png)

### Lovelace Demo Lysstyring Edit in YAML 

```yaml
square: false
columns: 1
type: grid
cards:
  - type: custom:simple-clock-card
    use_military: true
    hide_seconds: true
  - type: entities
    entities:
      - entity: light.ikea_e27_b7a411fe_level_light_color_on_off
    title: Ikea E27 LED 1924G9 - 704.391.58
    state_color: true
  - type: entities
    entities:
      - entity: binary_sensor.demo_ms01_iaszone_2
        name: eWeLink MS01
        secondary_info: last-changed
      - entity: sensor.demo_ms01_battery_2
        name: eWeLink  MS01 Battery
    state_color: true
    title: Sonoff Motion Sensor SNZB-03
  - type: entities
    entities:
      - entity: timer.demo_lys_timeout
        name: Helper Demo Lys Timeout
    state_color: true
  - type: entities
    entities:
      - entity: sensor.ewelink_wb01_19019723_power
      - entity: button.ewelink_wb01_19019723_identify
    title: Sonoff Wireless Switch SNZB-01
    state_color: true
```

## Automation

![Demo_Lysstyring_Auto_2022-10-22_19-20-55.png](./Images/Demo_Lysstyring_Auto_2022-10-22_19-20-55.png)

### Automation  **Demo Lys Styring** Edit in YAML

```yaml
alias: Demo Lys Styring
description: Lysstyring med Sonoff SNZB-01 & SNZB-03 Zigbee enheder og en Ikea E27 pærer
trigger:
  - type: motion
    platform: device
    device_id: 99209f9ae32fe0e766da839042ba7085
    entity_id: binary_sensor.demo_ms01_iaszone_2
    domain: binary_sensor
    id: Motion Start
  - type: no_motion
    platform: device
    device_id: 99209f9ae32fe0e766da839042ba7085
    entity_id: binary_sensor.demo_ms01_iaszone_2
    domain: binary_sensor
    id: Motion Stop
  - platform: event
    event_type: timer.finished
    event_data:
      entity_id: timer.demo_lys_timeout
    id: Timer Finished
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 3aef6197348e3af00998bce53891cb21
      command: toggle
    id: SNZB-01 Press Action
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 3aef6197348e3af00998bce53891cb21
      command: "on"
    id: SBZN-01 Double Press Action
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 3aef6197348e3af00998bce53891cb21
      command: "off"
    id: SBZN-01 Hold Action
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: Motion Start
        sequence:
          - service: timer.cancel
            data: {}
            target:
              entity_id: timer.demo_lys_timeout
          - if:
              - condition: state
                entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
                state: "off"
            then:
              - type: turn_on
                device_id: e1ad356de61e26d86b0ecb3f9e07cca3
                entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
                domain: light
                brightness_pct: 3
      - conditions:
          - condition: trigger
            id: Motion Stop
        sequence:
          - service: timer.start
            data:
              duration: "15"
            target:
              entity_id: timer.demo_lys_timeout
      - conditions:
          - condition: trigger
            id: Timer Finished
        sequence:
          - type: turn_off
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
      - conditions:
          - condition: trigger
            id: SNZB-01 Press Action
        sequence:
          - type: toggle
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
          - service: timer.start
            data:
              duration: "59"
            target:
              entity_id: timer.demo_lys_timeout
      - conditions:
          - condition: trigger
            id: SBZN-01 Double Press Action
        sequence:
          - type: turn_on
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
            brightness_pct: 50
          - service: timer.start
            data:
              duration: "30"
            target:
              entity_id: timer.demo_lys_timeout
      - conditions:
          - condition: trigger
            id: SBZN-01 Hold Action
        sequence:
          - service: timer.finish
            data: {}
            target:
              entity_id: timer.demo_lys_timeout
          - type: turn_off
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
mode: single

```