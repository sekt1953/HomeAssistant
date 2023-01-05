# Home

## Clock

```yaml
type: vertical-stack
cards:
  - type: custom:simple-clock-card
    use_military: true
    hide_seconds: true
```

## Light

```yaml
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_pir
        name: Køkken
        entity: binary_sensor.bad_ms01_iaszone
      - type: custom:button-card
        template:
          - header_light
        entity: light.kitchentablelight
        name: Køkken Bord
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        name: Spisekrog
        entity: light.ikea_of_sweden_tradfri_bulb_e27_cws_806lm_light
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_pir
        name: Entre
        entity: binary_sensor.bad_ms01_iaszone
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_pir
        name: Bad
        entity: binary_sensor.bad_ms01_iaszone
      - type: custom:button-card
        template:
          - header_light
        entity: light.tz3210_sroezl0s_ts0504b_light
        name: Bad loft
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: Stue
      - type: custom:button-card
        template:
          - header_light
        entity: light.tz3000_dbou1ap4_ts0505a_light
        name: Kohorn
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_pir
        entity: sensor.bad_ms01_battery
        name: Pir Bad
        show_state: true
        styles:
          card:
            - background-color: |
                [[[
                  if (states['sensor.bad_ms01_battery'].state >= 20)
                    return "green";
                  return "red";
                ]]]
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: null
```
