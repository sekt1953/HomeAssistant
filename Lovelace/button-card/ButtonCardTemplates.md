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

### header_0

```yaml
  header_0:
    aspect_ratio: 1.3
    color_type: card
    haptic: success
```

### header_timer

```yaml
  header_timer:
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
    show_last_changed: true
    show_state: false
    color: blue
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
          state:
            - color: yellow
            - font-size: 0px
      - value: 'on'
        styles:
          card:
            - color: yellow
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 15px
          icon:
            - color: yellow
          label:
            - font-size: 0px
            - color: yellow
          state:
            - color: yellow
            - font-size: 0px
```

### header_pir

```yaml
  header_pir:
    show_last_changed: true
    show_state: false
    color: blue
    state:
      - value: 'off'
        icon: mdi:human-male
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
          state:
            - color: yellow
            - font-size: 0px
      - value: 'on'
        styles:
          card:
            - color: yellow
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 15px
          icon:
            - color: yellow
          label:
            - font-size: 0px
            - color: yellow
          state:
            - color: yellow
            - font-size: 0px

```

## views

```yaml
views:
  - title: Home
    icon: mdi:home
[...]
```
