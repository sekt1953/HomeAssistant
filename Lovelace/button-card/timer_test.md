# button-card 

* Kilde: 
  * https://github.com/custom-cards/button-card
  * [Community guides:](https://github.com/custom-cards/button-card#community-guides)
    * https://robotnet.dk/2020/homekit-knapper-custom-buttons-home-assistant.html
  * [Credits](https://github.com/custom-cards/button-card#credits)
  *

## Kitchen-Timer

![Demo_000](./images/Sk%C3%A6rmbillede%20fra%202022-12-27%2005-13-56.png)

### Button Card Templates

Kilde: [Configuration Templates](https://github.com/custom-cards/button-card#configuration-templates)

```yaml
button_card_templates:
  variable_test:
    variables:
      var_name: null
    name: '[[[ return variables.var_name ]]]'
  header:
    aspect_ratio: 1.2
    color: red
    color_type: card
    haptic: success
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

### Vertical Stack Card Configuration

```yaml
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
[.. Line 1 ..]
  - type: horizontal-stack
    cards: 
[.. Line 2 ..]
  - type: horizontal-stack
    cards: 
[.. Line 3 ..]
  - type: horizontal-stack
    cards: 
```

### Line 1.1 Blødkogte æg

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name: Blødkogte Æg
entity: timer.kitchen_001_aeg_blodkogte
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_001_aeg_blodkogte
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_001_aeg_blodkogte
```

### Line 1.2 Hårdkogte Æg

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name: Hårdkogte Æg
entity: timer.kitchen_002_aeg_hardkogte
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_002_aeg_hardkogte
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_002_aeg_hardkogte
```

### Line 1.3 Morgen Boller Bagetid ved 220°C

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name: Morgen Boller<br>Bagetid ved 220°C
entity: timer.kitchen_010_morgen_boller_bagetid
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_010_morgen_boller_bagetid
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_010_morgen_boller_bagetid
```

### Line 2.1 Rugbrød hævetid

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name: Rugbrød hævetid
entity: timer.kitchen_003_rugbrod_haevetid
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_003_rugbrod_haevetid
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_003_rugbrod_haevetid
```

### Line 2.2 Rugbrød bagetid ved 170°C

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name: Rugbrød bagetid<br>ved 170°C
entity: timer.kitchen_004_rugbrod_bagetid
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_004_rugbrod_bagetid
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_004_rugbrod_bagetid
```

### Line 2.3 Empty card

```yaml
type: custom:button-card
template: variable_test
aspect_ratio: 1.2
```

### Line 3.1  Fødselsdagsboller hævetid 1 

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name:  Fødselsdagsboller hævetid 1 
entity: timer.kitchen_005_fodselsdagsboller_haevetid_1
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_005_fodselsdagsboller_haevetid_1
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_005_fodselsdagsboller_haevetid_1
```

### Line 3.2  Fødselsdagsboller hævetid 2 

```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name:  Fødselsdagsboller hævetid 2 
entity: timer.kitchen_006_fodselsdagsboller_haevetid_2
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_006_fodselsdagsboller_haevetid_2
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_006_fodselsdagsboller_haevetid_2
```

### Line 3.3 Fødselsdagsboller bagetid ved 200°C


```yaml
type: custom:button-card
template:
  - variable_test
  - header
variables:
  var_name:  Fødselsdagsboller bagetid ved 200°C
entity: timer.kitchen_007_fodselsdagsboller_bagetid
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_007_fodselsdagsboller_bagetid
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_007_fodselsdagsboller_bagetid
```




<hr>

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

### Helpers

![Helpers_000](./images/Sk%C3%A6rmbillede%20fra%202022-12-27%2005-40-39.png)
