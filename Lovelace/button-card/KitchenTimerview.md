# Kitchen Timer View

## Vertical Stack Card Configuration

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

## Line 1.

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

## Line 2.

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

## Line 3.

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

## Line 4.

### Line 4.1 

### Line 4.2 

### Line 4.3 