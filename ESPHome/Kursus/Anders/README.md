# Anders Demo

## Kode

```yaml
alias: New Automation1
description: ""
trigger:
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 41005df493e54013f16a89e96fb29926
      command: toggle
    id: press action
  - platform: event
    event_type: zha_event
    id: "motion "
    event_data:
      unique_id: 0c:43:14:ff:fe:19:41:3e:1:0x0005
      device_id: 41005df493e54013f16a89e96fb29926
      endpoint_id: 1
      cluster_id: 5
      command: press
      args:
        - 256
        - 13
        - 0
  - platform: event
    event_type: zha_event
    id: sluk
    event_data:
      device_id: 41005df493e54013f16a89e96fb29926
      endpoint_id: 1
      cluster_id: 5
      command: press
      args:
        - 257
        - 13
        - 0
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: press action
        sequence:
          - type: toggle
            device_id: 4becdf5c9115f57dfe8cfdb1a96b0fab
            entity_id: light.pwm_kokken_new_1
            domain: light
      - conditions:
          - condition: trigger
            id: "motion "
        sequence:
          - type: turn_on
            device_id: 4becdf5c9115f57dfe8cfdb1a96b0fab
            entity_id: light.pwm_kokken_new_2
            domain: light
            brightness_pct: 100
      - conditions:
          - condition: trigger
            id: sluk
        sequence:
          - type: turn_off
            device_id: 4becdf5c9115f57dfe8cfdb1a96b0fab
            entity_id: light.pwm_kokken_new_2
            domain: light
mode: single
```