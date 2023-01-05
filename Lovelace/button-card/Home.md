# Home

![Home](./images/Sk%C3%A6rmbillede%20fra%202023-01-05%2014-09-45.png)

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
        name: Spisekrog
        entity: light.ikea_of_sweden_tradfri_bulb_e27_cws_806lm_light
      - type: custom:button-card
        template:
          - header_light
        entity: null
        name: klima
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
        name: klima
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
          - header_grid_climate
        entity: null
        custom_fields:
          text_0: |
            [[[ return '<span>' + states['sensor.processor_temperature'].state + ' °C</span>' ]]]
          text_1: >
            [[[ return '<span>' + states['sensor.klima280_bme280_humidity'].state + ' %</b></span>' ]]]
          text_2: >
            [[[ return '<span>' + states['sensor.klima280_bme280_pressure'].state + ' hPa</b></span>' ]]]
          text_3: >
            [[[ return '<span>' + states['sensor.klima280_bh1750_illuminance'].state + ' lx</b></span>' ]]]
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

### Climate Card

```yaml
      - type: custom:button-card
        template:
          - header_grid_climate
        entity: null
        custom_fields:
          text_0: |
            [[[ return '<span>' + states['sensor.processor_temperature'].state + ' °C</span>' ]]]
          text_1: >
            [[[ return '<span>' + states['sensor.klima280_bme280_humidity'].state + ' %</b></span>' ]]]
          text_2: >
            [[[ return '<span>' + states['sensor.klima280_bme280_pressure'].state + ' hPa</b></span>' ]]]
          text_3: >
            [[[ return '<span>' + states['sensor.klima280_bh1750_illuminance'].state + ' lx</b></span>' ]]]
```