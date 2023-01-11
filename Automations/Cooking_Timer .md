# Cooking_Timer:

## Helpers:

* /config/timer_merge_named/kitchens.yaml

```yaml
# Cooking_Timer
cooking_001_aeg_blodkogte:
  name: "Æg Blødkogte"
  duration: 600
  icon: mdi:egg-easter

cooking_002_aeg_hardkogte:
  name: "Æg Hårdkogte"
  duration: 900
  icon: mdi:egg

cooking_003_rugbrod_haevetid:
  name: "Rugbrød hævetid"
  duration: 5400
  icon: mdi:bread-slice

cooking_004_rugbrod_bagetid:
  name: "Rugbrød bagetid ved 170°C"
  duration: 5400
  icon: mdi:bread-slice
  
cooking_005_fodselsdagsboller_haevetid_1:
  name: "Fødselsdagsboller hævetid 1"
  duration: 1200
  icon: mdi:volleyball
  
cooking_006_fodselsdagsboller_haevetid_2:
  name: "Fødselsdagsboller hævetid 2"
  duration: 3600
  icon: mdi:volleyball
  
cooking_007_fodselsdagsboller_bagetid:
  name: "Fødselsdagsboller bagetid ved 200°C"
  duration: 720
  icon: mdi:volleyball
  
cooking_008_grahamsbrod_haevetid:
  name: "Grahamsbrød Hævetid"
  duration: 5400
  icon: mdi:baguette
  
cooking_009_grahamsbrod_bagetid:
  name: "Grahamsbrød Bagetid ved 200°C"
  duration: 1500
  icon: mdi:baguette
  
cooking_010_morgen_boller_bagetid:
  name: "Morgen Boller Bagetid ved 220°C"
  duration: 1020
  icon: mdi:coffee-outline
```

## Scripts:

* /config/scripts.yaml - Cooking_Timer_Start

```yaml
alias: Cooking_Timer_Start
sequence:
  - if:
      - condition: template
        value_template: "{{ is_state(entity_id,'idle')}}"
    then:
      - service: timer.start
        data: {}
        target:
          entity_id: "{{entity_id}}"
mode: single
icon: mdi:timer
```

## Automations:

* /config/automations.yaml - Cooking_Timer Send Notification

```yaml
- id: '1673430497843'
  alias: Cooking_Timer Send Notification
  description: ''
  trigger:
  - platform: state
    entity_id:
    - timer.cooking_001_aeg_blodkogte
    - timer.cooking_002_aeg_hardkogte
    - timer.cooking_003_rugbrod_haevetid
    - timer.cooking_004_rugbrod_bagetid
    - timer.cooking_005_fodselsdagsboller_haevetid_1
    - timer.cooking_006_fodselsdagsboller_haevetid_2
    - timer.cooking_007_fodselsdagsboller_bagetid
    - timer.cooking_008_grahamsbrod_haevetid
    - timer.cooking_009_grahamsbrod_bagetid
    - timer.cooking_010_morgen_boller_bagetid
    from: active
    to: idle
  condition: []
  action:
  - service: notify.persistent_notification
    data:
      message: '{{ trigger.to_state.name }}'
      title: 'Køkken Timer Slut !! '
  - service: notify.sekt1953_group_1
    data:
      title: 'Køkken Timer Slut !! '
      message: '{{ trigger.to_state.name }}'
  mode: queued
  max: 10
```

## Lovelace:

### Kitchen:

#### UI-Template – button_card_templates: 
* header_nocard

```yaml
  header_nocard:
    aspect_ratio: 1.3
```

* header_0:

```yaml
  header_0:
    template: header_nocard
    color_type: card
    haptic: success
```

* header_cooking:

```yaml
  header_cooking:
    template: header_0
    color: red
    show_last_changed: false
    show_state: true
    tap_action:
      action: call-service
      service: script.cooking_timer_start
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

#### View - kitchen

```yaml
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
      - type: vertical-stack
        cards:
          - type: custom:simple-clock-card
            hide_seconds: true
            use_military: true
            font_size: 40px
            padding_size: 10px
      - type: vertical-stack
        cards:
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                icon: mdi:home
                tap_action:
                  action: navigate
                  navigation_path: /lovelace/0
                styles:
                  card:
                    - height: 40px
              - type: custom:button-card
                icon: mdi:chevron-down
                tap_action:
                  action: navigate
                  navigation_path: /lovelace/more
                styles:
                  card:
                    - height: 40px
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_cooking
        name: Blødkogte Æg
        entity: timer.cooking_001_aeg_blodkogte
      - type: custom:button-card
        template:
          - header_cooking
        name: Hårdkogte Æg
        entity: timer.cooking_002_aeg_hardkogte
      - type: custom:button-card
        template:
          - header_cooking
        name: Morgen Boller<br>Bagetid ved 220°C
        entity: timer.cooking_010_morgen_boller_bagetid
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_cooking
        name: Rugbrød hævetid
        entity: timer.cooking_003_rugbrod_haevetid
      - type: custom:button-card
        template:
          - header_cooking
        name: Rugbrød bagetid<br>ved 170°C
        entity: timer.cooking_004_rugbrod_bagetid
      - type: custom:button-card
        template:
          - header_nocard
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_cooking
        name: Boller hævetid 1
        entity: timer.cooking_005_fodselsdagsboller_haevetid_1
      - type: custom:button-card
        template:
          - header_cooking
        name: Boller hævetid 2
        entity: timer.cooking_006_fodselsdagsboller_haevetid_2
      - type: custom:button-card
        template:
          - header_cooking
        name: Boller bagetid<br>ved 200°C
        entity: timer.cooking_007_fodselsdagsboller_bagetid
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_cooking
        name: Grahamsbrød<br>Hævetid
        entity: timer.cooking_008_grahamsbrod_haevetid
      - type: custom:button-card
        template:
          - header_cooking
        name: Grahamsbrød<br>Bagetid ved 200°C
        entity: timer.cooking_009_grahamsbrod_bagetid
      - type: custom:button-card
        template:
          - header_nocard
  - type: custom:button-card
    color_type: blank-card
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_pir
        name: Køkken
        entity: binary_sensor.ewelink_ms01_iaszone_2
      - type: custom:button-card
        template:
          - header_light_bw
        entity: light.kitchen_old
        name: Køkken Old
      - type: custom:button-card
        template:
          - header_switch
        entity: switch.tz3000_upjrsxh1_ts011f_switch
        name: Ovn
        icon: mdi:spotlight
      - type: custom:button-card
        template:
          - header_light_color
        name: Spisekrog
        entity: light.ikea_of_sweden_tradfri_bulb_e27_cws_806lm_light
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_blue
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_light_bw
        entity: light.kitchentablelight
        name: Køkken New
      - type: custom:button-card
        template:
          - header_blue
        entity: null
        name: null
      - type: custom:button-card
        template:
          - header_blue
        entity: null
        name: null
```
