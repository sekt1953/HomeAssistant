# Demo Lysstyring med SNZB-01 & SNZB-03

Denne lysstyring har en Sonoff Wireless Switch SNZB-01 uden for døren, en Sonoff Motion Sensor SNZB-03 inde i lokalet og en lyskilde Ikea E27 LED1924G9.

* Et enkelt tryk på SNZB-01
  * Udløser toggle af lyskilden Ikea E27 og starter en timer "Demo Lys Timeout".
    * går du ikke ind i rummet og påvirker Motion Sensoren SNZB-03, vil lyses slukkes når timeren løber ud.
    * går du ind i rummet og påvirker Motion Sensoren SNZB-03, vil timeren blive nulstillet og Motion Sensoren SNZB-03 vil overtage styringen.
* Et dobbelt tryk på SNZB-01
  * Vil tænde lyskilden med en lysstyrke på 50%, og starte timeren "Demo Lys Timeout"
    * går du ikke ind i rummet og påvirker Motion Sensoren SNZB-03, vil lyses slukkes når timeren løber ud.
    * går du ind i rummet og påvirker Motion Sensoren SNZB-03, vil timeren blive nulstillet og Motion Sensoren SNZB-03 vil overtage styringen.
* Et langt tryk på SNZB-01
  * Vil nulstille timeren, og slukke lyset
    * NB!! går du ind i rummet før SNZB-03 er i clear tilstand vil lyset ikke tænde.
* Går du ind i rummet ude at påvirke trykknappen SNZB-01
  * Vil lyset tænde med en lysstyrke på 3% 
  * Når SNZB-03 er i clear mode vil den starte timeren
    * bliver SNZB-03 påvirket igen vil fimeren nulstille.
    * bliber SNZB-03 ikke påvirket igen vil lyset slukke når timeren løber ud.


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

## Helper Demo Lys Timeout

![Demo_Lysstyring_Helper_2022-10-22_20-49-21.png](./Images/Demo_Lysstyring_Helper_2022-10-22_20-49-21.png)

NB!! Fluenet i Restore feltet vil få timeren til at fortsætte efter en restart af Home Assistant, en god ting, se mere i timer dokumentationen link herunder.  
Home Assistant's Timer Dokumentation er [HER!!!](https://www.home-assistant.io/integrations/timer/)

## Automation

![Demo_Lysstyring_Auto_2022-10-22_19-20-55.png](./Images/Demo_Lysstyring_Auto_2022-10-22_19-20-55.png)

### Automation  **Demo Lys Styring** Edit in visual editor

#### Triggers

![Demo_Lysstyring_Trig_2022-10-22_19-34-00.png](./Images/Demo_Lysstyring_Trig_2022-10-22_19-34-00.png)  
![Demo_Lysstyring_Trig_2022-10-22_19-34-16.png](./Images/Demo_Lysstyring_Trig_2022-10-22_19-34-16.png)
![Demo_Lysstyring_Trig_2022-10-22_19-34-32.png](./Images/Demo_Lysstyring_Trig_2022-10-22_19-34-32.png)
![Demo_Lysstyring_Trig_2022-10-22_19-34-48.png](./Images/Demo_Lysstyring_Trig_2022-10-22_19-34-48.png)
![Demo_Lysstyring_Trig_2022-10-22_19-35-02.png](./Images/Demo_Lysstyring_Trig_2022-10-22_19-35-02.png)
![Demo_Lysstyring_Trig_2022-10-22_19-35-57.png](./Images/Demo_Lysstyring_Trig_2022-10-22_19-35-57.png)

#### Actions

##### Option 1:

![Demo_Lysstyring_Action1_2022-10-22_20-04-53.png](./Images/Demo_Lysstyring_Action1_2022-10-22_20-04-53.png)  
![Demo_Lysstyring_Action1_2022-10-22_20-05-44.png](./Images/Demo_Lysstyring_Action1_2022-10-22_20-05-44.png)  
![Demo_Lysstyring_Action1_2022-10-22_20-06-02.png](./Images/Demo_Lysstyring_Action1_2022-10-22_20-06-02.png)  

##### Option 2:

![](./Images/Demo_Lysstyring_Action2_2022-10-22_20-10-00.png)

##### Option 3:

![Demo_Lysstyring_Action3_2022-10-22_20-14-01.png](./Images/Demo_Lysstyring_Action3_2022-10-22_20-14-01.png)

##### Option 4:

![Demo_Lysstyring_Action4_2022-10-22_20-15-52.png](./Images/Demo_Lysstyring_Action4_2022-10-22_20-15-52.png)  
![Demo_Lysstyring_Action4_2022-10-22_20-16-08.png](./Images/Demo_Lysstyring_Action4_2022-10-22_20-16-08.png)  

##### Option 5:

![Demo_Lysstyring_Action5_2022-10-22_20-18-35.png](./Images/Demo_Lysstyring_Action5_2022-10-22_20-18-35.png)
![Demo_Lysstyring_Action5_2022-10-22_20-18-59.png](./Images/Demo_Lysstyring_Action5_2022-10-22_20-18-59.png)

##### Option 6:

![Demo_Lysstyring_Action6_2022-10-22_20-22-13.png](./Images/Demo_Lysstyring_Action6_2022-10-22_20-22-13.png)  
![Demo_Lysstyring_Action6_2022-10-22_20-22-47.png](./Images/Demo_Lysstyring_Action6_2022-10-22_20-22-47.png)  

### Automation  **Demo Lys Styring** Edit in YAML

```yaml
alias: Demo Lys Styring
description: Lysstyring med Sonoff SNZB-01 & SNZB-03 Zigbee enheder og en Ikea E27 pærer
trigger:
  - type: motion
    platform: device
    device_id: 99209f9ae32fe0e766da839042ba7085
    entity_id: binary_sensor.demo_ms01_iaszone_2
    domain: binary_sensor
    id: Motion Start
  - type: no_motion
    platform: device
    device_id: 99209f9ae32fe0e766da839042ba7085
    entity_id: binary_sensor.demo_ms01_iaszone_2
    domain: binary_sensor
    id: Motion Stop
  - platform: event
    event_type: timer.finished
    event_data:
      entity_id: timer.demo_lys_timeout
    id: Timer Finished
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 3aef6197348e3af00998bce53891cb21
      command: toggle
    id: SNZB-01 Press Action
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 3aef6197348e3af00998bce53891cb21
      command: "on"
    id: SBZN-01 Double Press Action
  - platform: event
    event_type: zha_event
    event_data:
      device_id: 3aef6197348e3af00998bce53891cb21
      command: "off"
    id: SBZN-01 Hold Action
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: Motion Start
        sequence:
          - service: timer.cancel
            data: {}
            target:
              entity_id: timer.demo_lys_timeout
          - if:
              - condition: state
                entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
                state: "off"
            then:
              - type: turn_on
                device_id: e1ad356de61e26d86b0ecb3f9e07cca3
                entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
                domain: light
                brightness_pct: 3
      - conditions:
          - condition: trigger
            id: Motion Stop
        sequence:
          - service: timer.start
            data:
              duration: "15"
            target:
              entity_id: timer.demo_lys_timeout
      - conditions:
          - condition: trigger
            id: Timer Finished
        sequence:
          - type: turn_off
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
      - conditions:
          - condition: trigger
            id: SNZB-01 Press Action
        sequence:
          - type: toggle
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
          - service: timer.start
            data:
              duration: "59"
            target:
              entity_id: timer.demo_lys_timeout
      - conditions:
          - condition: trigger
            id: SBZN-01 Double Press Action
        sequence:
          - type: turn_on
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
            brightness_pct: 50
          - service: timer.start
            data:
              duration: "30"
            target:
              entity_id: timer.demo_lys_timeout
      - conditions:
          - condition: trigger
            id: SBZN-01 Hold Action
        sequence:
          - service: timer.finish
            data: {}
            target:
              entity_id: timer.demo_lys_timeout
          - type: turn_off
            device_id: e1ad356de61e26d86b0ecb3f9e07cca3
            entity_id: light.ikea_e27_b7a411fe_level_light_color_on_off
            domain: light
mode: single

```
