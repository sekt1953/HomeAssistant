# Demo Lysstyring med SNZB-01 & SNZB-03

## Lovelace Demo Lysstyring

![](./Images/Demo_Lysstyring_2022-10-22_17-53-09.png)

### Lovelace Demo Lysstyring Edit in visual editor

![Demo_Lysstyring_Love_2022-10-22_17-54-54.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-54-54.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-03.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-03.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-11.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-11.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-17.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-17.png)
![Demo_Lysstyring_Love_2022-10-22_17-55-24.png](./Images/Demo_Lysstyring_Love_2022-10-22_17-55-24.png)

### Lovelace Demo Lysstyring Edit in YAML 

```yaml
square: false
columns: 1
type: grid
cards:
  - type: custom:simple-clock-card
    use_military: true
    hide_seconds: true
  - type: entities
    entities:
      - entity: light.ikea_e27_b7a411fe_level_light_color_on_off
    title: Ikea E27 LED 1924G9 - 704.391.58
    state_color: true
  - type: entities
    entities:
      - entity: binary_sensor.demo_ms01_iaszone_2
        name: eWeLink MS01
        secondary_info: last-changed
      - entity: sensor.demo_ms01_battery_2
        name: eWeLink  MS01 Battery
    state_color: true
    title: Sonoff Motion Sensor SNZB-03
  - type: entities
    entities:
      - entity: timer.demo_lys_timeout
        name: Helper Demo Lys Timeout
    state_color: true
  - type: entities
    entities:
      - entity: sensor.ewelink_wb01_19019723_power
      - entity: button.ewelink_wb01_19019723_identify
    title: Sonoff Wireless Switch SNZB-01
    state_color: true
```
