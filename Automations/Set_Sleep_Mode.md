# Set Sleep Mode

```yaml
alias: "Set Sleep Mode"
description: ""
trigger:
  - type: plugged_in
    platform: device
    device_id: 0f7ca4cd333bf32d57e15ec987334e7a
    entity_id: binary_sensor.sm_a226b_is_charging
    domain: binary_sensor
    id: Sleep Mode On
condition: null
action:
  - choose:
      - conditions:
          - condition: trigger
            id: Sleep Mode On
          - condition: state
            entity_id: sensor.sekt_sm_a226b
            state: kitchen
          - condition: state
            entity_id: binary_sensor.night
            state: "on"
        sequence:
          - service: input_boolean.turn_on
            data: {}
            target:
              entity_id: input_boolean.sleep
mode: single

```
