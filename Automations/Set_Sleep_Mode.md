# Sleep Mode

## Automation - Set Sleep Mode

```yaml
alias: Set Sleep Mode
description: ""
trigger:
  - type: plugged_in
    platform: device
    device_id: 0f7ca4cd333bf32d57e15ec987334e7a
    entity_id: binary_sensor.sm_a226b_is_charging
    domain: binary_sensor
    id: Sleep Mode On
  - platform: state
    entity_id:
      - binary_sensor.nosun
    to: "on"
    from: "off"
    id: Sun up
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
      - conditions:
          - condition: trigger
            id: Sun up
        sequence:
          - service: input_boolean.turn_off
            data: {}
            target:
              entity_id: input_boolean.sleep
mode: single
```

## Script - Sleep Mode Change

```yaml
alias: Sleep Mode Change
sequence:
  - if:
      - condition: state
        entity_id: input_boolean.sleep
        state: "on"
    then:
      - service: light.turn_off
        data: {}
        target:
          entity_id:
            - light.sleep_mode_light_off
      - service: switch.turn_off
        data: {}
        target:
          entity_id: switch.skarme_ts0101_switch
mode: single
icon: mdi:sleep
```

## Helpers Group Light 

* [Managing groups](https://www.home-assistant.io/integrations/group/#managing-groups)
  * [BINARY SENSOR, LIGHT, AND SWITCH GROUPS](https://www.home-assistant.io/integrations/group/#binary-sensor-light-and-switch-groups)

![Managing groups](./Images/Sk%C3%A6rmbillede%20fra%202023-01-09%2022-24-05.png)

* [GROUP OPTIONS](https://www.home-assistant.io/integrations/group/#group-options)

![group-options](./Images/Sk%C3%A6rmbillede%20fra%202023-01-09%2022-22-10.png)
