# Presence

## Sleep Mode

### Helpers:

#### Group - Times Of the Day

* /config/binary_sensor_merge_list/times_of_the_day.yaml

```yaml
  - platform: tod
    name: Morning
    after: "06:00"
    before: "08:00"

  - platform: tod
    name: Late Morning
    after: "08:00"
    before: "10:00"

  - platform: tod
    name: Day Time
    after: "10:00"
    before: "17:00"

  - platform: tod
    name: Dinner Time
    after: "17:00"
    before: "20:00"

  - platform: tod
    name: Evening
    after: "20:00"
    before: "21:30"

  - platform: tod
    name: Night
    after: "21:30"
    before: "06:00"
```

#### Group Sleep Mode Light Off

* [Managing groups](https://www.home-assistant.io/integrations/group/#managing-groups)
  * [BINARY SENSOR, LIGHT, AND SWITCH GROUPS](https://www.home-assistant.io/integrations/group/#binary-sensor-light-and-switch-groups)

![Managing groups](./Images/Sk%C3%A6rmbillede%20fra%202023-01-09%2022-24-05.png)

* [GROUP OPTIONS](https://www.home-assistant.io/integrations/group/#group-options)

![group-options](./Images/Sk%C3%A6rmbillede%20fra%202023-01-09%2022-22-10.png)

### Sensor:

#### Espresense:

* Kilde:
  * [ESPresense](https://espresense.com/)

* /config/sensor_merge_list/espresense.yaml

```yaml
# ESPresense https://espresense.com
# One entry for each beacon you want to track
  - platform: mqtt_room
    name: 'SEKT-LG-K500n'
    state_topic: 'espresense/rooms'
    device_id: "iBeacon:ac133e90-4f30-46ce-b107-131578bcf868-100-1"
    timeout: 5
    away_timeout: 120 # number of seconds after which the enitity will get status not_home

  - platform: mqtt_room
    name: 'SEKT-SM-A226B'
    state_topic: 'espresense/rooms'
    device_id: "iBeacon:61628813-8b1f-40dd-949f-13a709c25fbe-100-1"
    timeout: 5
    away_timeout: 120 # number of seconds after which the enitity will get status not_home
```

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
      - binary_sensor.night
    from: "on"
    to: "off"
    id: Sleep Mode Off
  - platform: state
    entity_id:
      - input_boolean.sleep
    from: "off"
    to: "on"
    id: Manual On
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
          - service: light.turn_off
            data: {}
            target:
              entity_id: light.sleep_mode_light_off
          - service: switch.turn_off
            data: {}
            target:
              entity_id: switch.sleep_mode_switch_off
      - conditions:
          - condition: trigger
            id: Sleep Mode Off
        sequence:
          - service: input_boolean.turn_off
            data: {}
            target:
              entity_id: input_boolean.sleep
          - if:
              - condition: state
                entity_id: sun.sun
                state: below_horizon
            then:
              - service: light.turn_on
                data:
                  kelvin: 2000
                  brightness_pct: 50
                target:
                  entity_id: light.frontdoor_ts0502a_light
      - conditions:
          - condition: trigger
            id: Manual On
        sequence:
          - service: light.turn_off
            data: {}
            target:
              entity_id: light.sleep_mode_light_off
          - service: switch.turn_off
            data: {}
            target:
              entity_id: switch.sleep_mode_switch_off
mode: single
```
## Lovelace:

### Template:

#### header_nocard:

```yaml
header_nocard:
  header_nocard:
    aspect_ratio: 1.3
```

```yaml
header_0:
  header_0:
    template: header_nocard
    color_type: card
    haptic: success
```

```yaml
header_blue:
  header_blue:
    template: header_0
    color: blue
    show_last_changed: false
    show_state: false
    state:
      - value: 'off'
        styles:
          card:
            - background-color: blue
            - filter: opacity(55%)
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 14px
          icon:
            - color: gray
          label:
            - font-size: 0px
            - color: yellow
      - value: 'on'
        styles:
          card:
            - background-color: '#000044'
            - color: yellow
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 15px
          label:
            - font-size: 11px
            - color: yellow
```

```yaml
header_input_boolean:
  header_input_boolean:
    template: header_blue
    show_last_changed: false
    styles:
      icon:
        - color: var(--button-card-light-color)
    tap_action:
      action: call-service
      service: input_boolean.toggle
      service_data:
        entity_id: entity
```

## View:

![Presence](./Images/Sk%C3%A6rmbillede%20fra%202023-01-11%2015-31-20.png)

```yaml
type: custom:button-card
template:
  - header_input_boolean
entity: input_boolean.sleep
name: null
icon: mdi:sleep
```
