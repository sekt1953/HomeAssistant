# Button Card Templates

Kilde: [Configuration Templates](https://github.com/custom-cards/button-card#configuration-templates)

* **managed** changes are managed by lovelace ui - add the template configuration to configuration in raw editor
  * go to your dashboard
  * click three dots and Edit dashboard button
  * click three dots again and click Raw configuration editor button
* **yaml** - add template configuration to your ui-lovelace.yaml

## ui-lovelace.yaml

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
            - color: yellow
            - '--mdc-ripple-color': blue
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 16px
          icon:
            - color: yellow
          label:
            - font-size: 11px
            - color: yellow
          state:
            - color: yellow

[...]