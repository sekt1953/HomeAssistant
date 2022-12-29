# Kitchen Timer View

## Vertical Stack Card Configuration

```yaml
type: vertical-stack
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
[.. Line 4 ..]
  - type: horizontal-stack
    cards: 
[.. Line 5 ..]
[.. Line 6 ..]
  - type: horizontal-stack
    cards: 
[.. Line 7 ..]
  - type: horizontal-stack
    cards: 
[.. Line 8 ..]
  - type: horizontal-stack
    cards: 
```

## Line 1

```yaml
type: custom:simple-clock-card
use_military: true
hide_seconds: false
```

## Line 2

### Line 2.1 Blødkogte æg

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name: Blødkogte Æg
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

### Line 2.2 Hårdkogte Æg

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name: Hårdkogte Æg
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

### Line 2.3 Morgen Boller Bagetid ved 220°C

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name: Morgen Boller<br>Bagetid ved 220°C
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

## Line 3

### Line 3.1 Rugbrød hævetid

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name: Rugbrød hævetid
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

### Line 3.2 Rugbrød bagetid ved 170°C

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name: Rugbrød bagetid<br>ved 170°C
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

### Line 3.3 Empty card

```yaml
type: custom:button-card
aspect_ratio: 1.2
```

## Line 4

### Line 4.1  Fødselsdagsboller hævetid 1 

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name:  Fødselsdagsboller hævetid 1 
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

### Line 4.2  Fødselsdagsboller hævetid 2 

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name:  Fødselsdagsboller hævetid 2 
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

### Line 4.3 Fødselsdagsboller bagetid ved 200°C

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name:  Fødselsdagsboller bagetid ved 200°C
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

## Line 5

### Line 5.1  Grahamsbrød Hævetid 

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name:   Grahamsbrød<br>Hævetid 
entity: timer.kitchen_008_grahamsbrod_haevetid
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_008_grahamsbrod_haevetid
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_008_grahamsbrod_haevetid
```

### Line 5.2   Grahamsbrød Bagetid ved 200°C 

```yaml
type: custom:button-card
template:
  - header_0
  - header_timer
name:   Grahamsbrød<br>Bagetid ved 200°C 
entity: timer.kitchen_009_grahamsbrod_bagetid
tap_action:
  action: call-service
  service: script.timerstart
  service_data:
    entity_id: timer.kitchen_009_grahamsbrod_bagetid
hold_action:
  action: call-service
  service: timer.cancel
  service_data:
    entity_id: timer.kitchen_009_grahamsbrod_bagetid
```

### Line 5.3

```yaml
type: custom:button-card
aspect_ratio: 1.2
```

### Line 6

```yaml
type: custom:button-card
color_type: blank-card
```

### Line 7

### Line 7.1

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
entity: light.kitchentablelight
name: Køkken Bord
```

### Line 7.2

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
name: Køkken Loft
```

### Line 7.3

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
name: Spisekrog
entity: light.ikea_of_sweden_tradfri_bulb_e27_cws_806lm_light
```

### Line 7.4

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
name: Korridor
```

### Line 8

### Line 8.1

```yaml
type: custom:button-card
template:
  - header_0
  - header_pir
name: Bad
entity: binary_sensor.bad_ms01_iaszone
```

### Line 8.2

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
```

### Line 8.3

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
```

### Line 8.4

```yaml
type: custom:button-card
template:
  - header_0
  - header_light
```
