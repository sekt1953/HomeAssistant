# Presence - Away Mode

## Automation - Set Away Mode

```yaml
alias: Set Away Mode
description: ""
trigger:
  - platform: state
    entity_id:
      - sensor.sekt_sm_a226b
    id: not_office
    from: office
    to: not_home
    for:
      hours: 0
      minutes: 0
      seconds: 30
  - platform: state
    entity_id:
      - sensor.sekt_sm_a226b
    id: not_kitchen
    from: kitchen
    to: not_home
    for:
      hours: 0
      minutes: 0
      seconds: 30
  - platform: state
    entity_id:
      - sensor.sekt_sm_a226b
    id: not_living
    from: living_room
    to: not_home
    for:
      hours: 0
      minutes: 0
      seconds: 30
  - platform: state
    entity_id:
      - input_boolean.away
    to: "on"
    from: "off"
    id: Manual Away
    for:
      hours: 0
      minutes: 0
      seconds: 30
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: Manual Away
        sequence:
          - service: notify.persistent_notification
            data:
              title: Alarm
              message: Alarm Manual slået til
          - service: notify.sekt1953_group_1
            data:
              title: Alarm Status
              message: Alarm Manual slået til
            enabled: true
      - conditions:
          - condition: or
            conditions:
              - condition: trigger
                id: not_office
              - condition: trigger
                id: not_kitchen
              - condition: trigger
                id: not_living
        sequence:
          - service: input_boolean.turn_on
            data: {}
            target:
              entity_id: input_boolean.away
          - service: notify.persistent_notification
            data:
              title: Alarm
              message: Automatisk slået til
          - service: notify.sekt1953_group_1
            data:
              title: Alarm Status
              message: Automatisk slået til
            enabled: true
  - service: light.turn_off
    data: {}
    target:
      entity_id: light.sleep_mode_light_off
mode: single
```
