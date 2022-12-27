# button-card 

* Kilde: 
  * https://github.com/custom-cards/button-card
  * [Community guides:](https://github.com/custom-cards/button-card#community-guides)
    * https://robotnet.dk/2020/homekit-knapper-custom-buttons-home-assistant.html
  * [Credits](https://github.com/custom-cards/button-card#credits)
  *

## Kitchen-Timer

![Demo_000](./images/Sk%C3%A6rmbillede%20fra%202022-12-27%2005-13-56.png)

### Vertical Stack Card Configuration

```yaml
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
```

### Blødkogte æg

```yaml
type: custom:button-card
aspect_ratio: 1.2
color: red
color_type: card
entity: timer.kitchen_001_aeg_blodkogte
name: Blødkogte æg
haptic: success
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    thetimer: timer.kitchen_001_aeg_blodkogte
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_001_aeg_blodkogte
show_last_changed: true
show_state: true
state:
  - value: idle
    styles:
      card:
        - filter: opacity(50%)
        - '--mdc-ripple-color': blue
        - '--mdc-ripple-press-opacity': 0.5
        - font-size: 14px
      icon:
        - filter: grayscale(100%)
      label:
        - font-size: 11px
  - value: active
    styles:
      card:
        - color: yellow
        - '--mdc-ripple-color': yellow
        - '--mdc-ripple-press-opacity': 0.5
        - font-size: 16px
      icon:
        - color: yellow
      label:
        - font-size: 11px
```

### Hårdkogte æg

```yaml
type: custom:button-card
aspect_ratio: 1.2
color: red
color_type: card
entity: timer.kitchen_002_aeg_hardkogte
name: Hårdkogte æg
haptic: success
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    thetimer: timer.kitchen_002_aeg_hardkogte
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_002_aeg_hardkogte
show_last_changed: true
show_state: true
state:
  - value: idle
    styles:
      card:
        - filter: opacity(50%)
        - '--mdc-ripple-color': blue
        - '--mdc-ripple-press-opacity': 0.5
        - font-size: 14px
      icon:
        - filter: grayscale(100%)
      label:
        - font-size: 11px
  - value: active
    styles:
      card:
        - color: blue
        - '--mdc-ripple-color': yellow
        - '--mdc-ripple-press-opacity': 0.5
        - font-size: 16px
      icon:
        - color: blue
      label:
        - font-size: 11px
        - color: blue
      state:
        - color: blue
```

## Script

### TimerStart

```yaml
alias: TimerStart
sequence:
  - if:
      - condition: template
        value_template: "{{ is_state(thetimer,'idle')}}"
    then:
      - service: timer.start
        data: {}
        target:
          entity_id: "{{thetimer}}"
mode: single
icon: mdi:timer
```