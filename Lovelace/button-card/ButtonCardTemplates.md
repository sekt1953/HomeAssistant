# Button Card Templates

## Kilde:

* [Configuration Templates](https://github.com/custom-cards/button-card#configuration-templates)

* **managed** changes are managed by lovelace ui - add the template configuration to configuration in raw editor
  * go to your dashboard
  * click three dots and Edit dashboard button
  * click three dots again and click Raw configuration editor button
* **yaml** - add template configuration to your ui-lovelace.yaml

## ui-lovelace.yaml

### button_card_templates

```yaml
button_card_templates:
```

### header_nocard

```yaml
  header_nocard:
    aspect_ratio: 1.3
```

### header_0

```yaml
  header_0:
    template: header_nocard
    color_type: card
    haptic: success
```

### header_blue

```yaml
  header_blue:
    template: header_0
    color: blue
    show_last_changed: true
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

```

### header_light

```yaml
    template: header_blue
    styles:
      icon:
        - color: var(--button-card-light-color-no-temperature)
```

### header_pir

```yaml
  header_pir:
    template: header_blue
    state:
      - value: 'on'
        styles:
          icon:
            - color: yellow
```

### header_timer

```yaml
  header_timer:
    template: header_0
    color: red
    show_last_changed: false
    show_state: true
    tap_action:
      action: call-service
      service: script.timerstart
      service_data:
        entity_id: entity
    hold_action:
      action: call-service
      service: timer.cancel
      service_data:
        entity_id: entity
    state:
      - value: idle
        styles:
          card:
            - filter: opacity(85%)
            - '--mdc-ripple-color': blue
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 14px
          icon:
            - color: gray
          label:
            - font-size: 10px
            - color: yellow
          state:
            - color: yellow
            - font-size: 0px
      - value: active
        styles:
          card:
            - color: yellow
            - '--mdc-ripple-color': blue
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 14px
          icon:
            - color: yellow
          label:
            - font-size: 10px
            - color: yellow
          state:
            - color: yellow
            - font-size: 14px
```

### header_grid_4

```yaml
  header_grid_4:
    template: header_0
    color: blue
    name: ''
    tap_action:
      action: navigate
      navigation_path: /lovelace/climate
    styles:
      card:
        - background-color: '#000044'
        - padding: 5%
        - color: ivory
        - font-size: 11px
        - text-shadow: 0px 0px 5px black
      custom_fields:
        label_0:
          - align-self: center
          - justify-self: start
        text_0:
          - align-self: center
          - justify-self: end
        label_1:
          - align-self: center
          - justify-self: start
        text_1:
          - align-self: center
          - justify-self: end
        label_2:
          - align-self: center
          - justify-self: start
        text_2:
          - align-self: center
          - justify-self: end
        label_3:
          - align-self: center
          - justify-self: start
        text_3:
          - align-self: center
          - justify-self: end
```

### header_grid_4_lux

```yaml
  header_grid_4_lux:
    template: header_grid_4
    styles:
      grid:
        - grid-template-areas: '"label_0 text_0" "label_1 text_1"  "label_2 text_2" "label_3 text_3"'
        - grid-template-columns: 1fr 1fr
        - grid-template-rows: 1fr 1fr 1fr 1fr
    custom_fields:
      label_0: >
        [[[ return `<ha-icon icon="mdi:thermometer"
        style="width:15px;"></ha-icon>` ]]]
      label_1: >
        [[[ return '<ha-icon icon="mdi:water-percent"
        style="width:15px;"></ha-icon>' ]]]
      label_2: >
        [[[ return '<ha-icon icon="mdi:gauge" style="width:15px;"></ha-icon>'
        ]]]
      label_3: >
        [[[ return '<ha-icon icon="mdi:weather-sunny"
        style="width:15px;"></ha-icon>' ]]]
```

### header_grid_4_name

```yaml
  header_grid_4_name:
    template: header_grid_4
    styles:
      grid:
        - grid-template-areas: '"n n" "label_1 text_1"  "label_2 text_2" "label_3 text_3"'
        - grid-template-columns: 1fr 1fr
        - grid-template-rows: 1fr 1fr 1fr 1fr
      name:
        - align-self: center
        - justify-self: start
        - font-weight: bold
    custom_fields:
      label_1: >
        [[[ return `<ha-icon icon="mdi:thermometer"
        style="width:15px;"></ha-icon>` ]]]
      label_2: >
        [[[ return '<ha-icon icon="mdi:water-percent"
        style="width:15px;"></ha-icon>' ]]]
      label_3: >
        [[[ return '<ha-icon icon="mdi:gauge" style="width: 15px;"></ha-icon>'
        ]]]
```

### header_grid_climate

```yaml
header_grid_climate:
    template: header_0
    color: blue
    name: ''
    tap_action:
      action: navigate
      navigation_path: /lovelace/climate
    styles:
      card:
        - background-color: '#000044'
        - padding: 5%
        - color: ivory
        - font-size: 11px
        - text-shadow: 0px 0px 5px black
      grid:
        - grid-template-areas: '"label_0 text_0" "label_1 text_1"  "label_2 text_2" "label_3 text_3"'
        - grid-template-columns: 1fr 1fr
        - grid-template-rows: 1fr 1fr 1fr 1fr
      custom_fields:
        label_0:
          - align-self: center
          - justify-self: start
        text_0:
          - align-self: center
          - justify-self: end
        label_1:
          - align-self: center
          - justify-self: start
        text_1:
          - align-self: center
          - justify-self: end
        label_2:
          - align-self: center
          - justify-self: start
        text_2:
          - align-self: center
          - justify-self: end
        label_3:
          - align-self: center
          - justify-self: start
        text_3:
          - align-self: center
          - justify-self: end
    custom_fields:
      label_0: >
        [[[ return `<ha-icon icon="mdi:thermometer" style="width:
        15px;"></ha-icon>` ]]]
      label_1: >
        [[[ return '<ha-icon icon="mdi:water-percent" style="width:
        15px;"></ha-icon>' ]]]
      label_2: >
        [[[ return '<ha-icon icon="mdi:gauge" style="width: 15px;"></ha-icon>'
        ]]]
      label_3: >
        [[[ return '<ha-icon icon="mdi:weather-sunny"
        style="width:15px;"></ha-icon>' ]]]
  ```

### header_grid

```yaml
  header_grid:
    aspect_ratio: 1.5/1
    styles:
      card:
        - background-color: '#000044'
        - padding: 5%
        - color: ivory
        - font-size: 15px
        - text-shadow: 0px 0px 5px black
      grid:
        - grid-template-areas: >-
            "label_0 text_0" "label_1 text_1" "label_2 text_2" "label_3 text_3"
            "label_4 text_4" "label_5 text_5" "label_6 text_6" "label_7 text_7"
            "label_8 text_8" "label_9 text_9"
        - grid-template-columns: 1.5fr 1fr
        - grid-template-rows: 2fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr
      custom_fields:
        label_0:
          - align-self: center
          - justify-self: start
        text_0:
          - align-self: center
          - justify-self: end
        label_1:
          - align-self: center
          - justify-self: start
        text_1:
          - align-self: center
          - justify-self: end
        label_2:
          - align-self: center
          - justify-self: start
        text_2:
          - align-self: center
          - justify-self: end
        label_3:
          - align-self: center
          - justify-self: start
        text_3:
          - align-self: center
          - justify-self: end
        label_4:
          - align-self: center
          - justify-self: start
        text_4:
          - align-self: center
          - justify-self: end
        label_5:
          - align-self: center
          - justify-self: start
        text_5:
          - align-self: center
          - justify-self: end
        label_6:
          - align-self: center
          - justify-self: start
        text_6:
          - align-self: center
          - justify-self: end
        label_7:
          - font-size: 25px
          - align-self: center
          - justify-self: start
        text_7:
          - align-self: center
          - justify-self: end
        label_8:
          - align-self: center
          - justify-self: start
        text_8:
          - align-self: center
          - justify-self: end
        label_9:
          - align-self: center
          - justify-self: start
        text_9:
          - align-self: center
          - justify-self: end
        label_n:
          - font-size: 20px
          - font-weight: bold
          - align-self: start
          - justify-self: start
        text_n:
          - align-self: center
          - justify-self: end
```

## views

```yaml
views:
  - title: Home
    icon: mdi:home
[...]
```
