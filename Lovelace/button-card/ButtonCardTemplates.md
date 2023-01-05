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
            - filter: opacity(50%)
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

### header_light

```yaml
  header_light:
    template: header_0
    color: blue
    styles:
      icon:
        - color: var(--button-card-light-color-no-temperature)
    state:
      - value: 'off'
        styles:
          card:
            - background-color: blue
            - filter: opacity(50%)
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
            - color: yellow
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 15px
          label:
            - font-size: 0px
            - color: yellow
```

### header_pir

```yaml
  header_pir:
    template: header_0
    color: blue
    show_last_changed: true
    show_state: false
    state:
      - value: 'off'
        icon: mdi:motion-sensor-off
        styles:
          card:
            - background-color: blue
            - filter: opacity(50%)
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 14px
          icon:
            - color: gray
      - value: 'on'
        icon: mdi:motion-sensor
        styles:
          card:
            - color: yellow
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 15px
          icon:
            - color: yellow
```

### header_grid_klima

```yaml
  header_grid_klima:
    template: header_0
    color: blue
    name: ''
    styles:
      card:
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
```

### header_grid

```yaml
  header_grid:
    aspect_ratio: 1.5/1
    styles:
      card:
        - background-color: '#000044'
        - border-radius: 1%
        - padding: 5%
        - color: ivory
        - font-size: 15px
        - text-shadow: 0px 0px 5px black
        - text-transform: capitalize
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
