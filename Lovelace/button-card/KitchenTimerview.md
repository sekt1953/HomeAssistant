# Kitchen Timer View

## Clomplet Raw KitchenTimerView.yaml

[Download Raw KitchenTimerView.yaml](./Raw/KitchenTimerView.yaml)

## Clock

### Clock - View image

![](./images/Sk%C3%A6rmbillede%20fra%202023-01-03%2000-17-44.png)

### Clock - View yaml

```yaml
type: custom:simple-clock-card
use_military: true
hide_seconds: false
```

## Timer

### Timer - View image

![Timer - View image](./images/Sk%C3%A6rmbillede%20fra%202023-01-03%2000-34-21.png)

### Timer - View yaml

```yaml
type: vertical-stack
cards:
  - type: custom:simple-clock-card
    use_military: true
    hide_seconds: false
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_timer
        name: Blødkogte Æg
        entity: timer.kitchen_001_aeg_blodkogte
      - type: custom:button-card
        template:
          - header_timer
        name: Hårdkogte Æg
        entity: timer.kitchen_002_aeg_hardkogte
      - type: custom:button-card
        template:
          - header_timer
        name: Morgen Boller<br>Bagetid ved 220°C
        entity: timer.kitchen_010_morgen_boller_bagetid
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_timer
        name: Rugbrød hævetid
        entity: timer.kitchen_003_rugbrod_haevetid
      - type: custom:button-card
        template:
          - header_timer
        name: Rugbrød bagetid<br>ved 170°C
        entity: timer.kitchen_004_rugbrod_bagetid
      - type: custom:button-card
        template:
          - header_nocard
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_timer
        name: Boller hævetid 1
        entity: timer.kitchen_005_fodselsdagsboller_haevetid_1
      - type: custom:button-card
        template:
          - header_timer
        name: Boller hævetid 2
        entity: timer.kitchen_006_fodselsdagsboller_haevetid_2
      - type: custom:button-card
        template:
          - header_timer
        name: Boller bagetid<br>ved 200°C
        entity: timer.kitchen_007_fodselsdagsboller_bagetid
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_timer
        name: Grahamsbrød<br>Hævetid
        entity: timer.kitchen_008_grahamsbrod_haevetid
      - type: custom:button-card
        template:
          - header_timer
        name: Grahamsbrød<br>Bagetid ved 200°C
        entity: timer.kitchen_009_grahamsbrod_bagetid
      - type: custom:button-card
        template:
          - header_nocard
  - type: custom:button-card
    color_type: blank-card

```

## Light

### Light - View image

![Light - View image](./images/Sk%C3%A6rmbillede%20fra%202023-01-03%2000-31-42.png)

### Light - View yaml

```yaml
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_light_bw
        entity: light.kitchentablelight
        name: Køkken Bord
      - type: custom:button-card
        template:
          - header_light_color
        name: Køkken Loft
      - type: custom:button-card
        template:
          - header_light_color
        name: Spisekrog
        entity: light.ikea_of_sweden_tradfri_bulb_e27_cws_806lm_light
      - type: custom:button-card
        template:
          - header_blue
        name: Korridor
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_pir
        name: Bad
        entity: binary_sensor.bad_ms01_iaszone
      - type: custom:button-card
        template:
          - header_blue
      - type: custom:button-card
        template:
          - header_blue
      - type: custom:button-card
        template:
          - header_blue```
