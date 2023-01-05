# Server 

## Intro

* Clock
  * As on my other pages, I always have a clock at the top, so you always have easy access to the time. As a clock I use a **HACS Frontend simple-clock-card**
* Samba-Backup
  * For my design of the **samba backup view**, I have used [ADVANCED styling options](https://github.com/custom-cards/button-card#advanced-styling-options) and got a lot of help from the page [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/), a slightly messy page, but full of good information.  
* Raspberry Pi 4

## Clock

### Clock - View image

![](./images/Sk%C3%A6rmbillede%20fra%202023-01-02%2021-50-21.png)

### Clock - View yaml-code

```yaml
type: vertical-stack
cards:
  - type: custom:simple-clock-card
    use_military: true
    hide_seconds: true
```

## Samba Backup

### Samba Backup - View images

![Samba-Backup](./images/Sk%C3%A6rmbillede%20fra%202023-01-02%2022-50-12.png)

### Samba Backup - View yaml-code

```yaml
  - type: horizontal-stack
    cards:
      - type: vertical-stack
        cards:
          - type: custom:button-card
            template:
              - header_grid
            entity: sensor.samba_backup
            icon: mdi:upload-network
            aspect_ratio: 2/1
            name: Samba Backup
            styles:
              grid:
                - grid-template-areas: >-
                    "n sb_status"     "sb_Last_backup_label sb_Last_backup"
                    "sb_backup_local_label sb_backup_local"  
                    "sb_backup_remote_label sb_backup_remote" 
                    "sb_total_backup_succeeded_label sb_total_backup_succeeded" 
                    "sb_total_backup_failed_label sb_total_backup_failed"
                - grid-template-columns: 1.5fr 1fr
                - grid-template-rows: 2fr 1fr 1fr 1fr 1fr 1fr
              name:
                - font-size: 20px
                - font-weight: bold
                - color: |
                    [[[
                      if (entity.state == 'IDLE') return 'white';
                      if (entity.state == 'SUCCEEDED') return 'green';
                      else return 'lime';
                    ]]]
                - align-self: start
                - justify-self: start
              img_cell:
                - justify-content: start
                - align-items: start
                - margin: none
              icon:
                - color: |
                    [[[
                      if (entity.state == 'IDLE') return 'white';
                      else return 'red';
                    ]]]
                - width: 70%
                - margin-top: '-10%'
              custom_fields:
                sb_status:
                  - color: |
                      [[[
                        if (entity.state == 'IDLE') return 'white';
                        if (entity.state == 'SUCCEEDED') return 'green';
                        else return 'lime';
                      ]]]
                  - font-size: 25px
                  - font-weight: bold
                  - align-self: start
                  - justify-self: end
                sb_Last_backup_label:
                  - align-self: center
                  - justify-self: start
                sb_Last_backup:
                  - align-self: center
                  - justify-self: end
                sb_backup_local_label:
                  - align-self: center
                  - justify-self: start
                sb_backup_local:
                  - align-self: center
                  - justify-self: end
                sb_backup_remote_label:
                  - align-self: center
                  - justify-self: start
                sb_backup_remote:
                  - align-self: center
                  - justify-self: end
                sb_total_backup_succeeded_label:
                  - align-self: center
                  - justify-self: start
                sb_total_backup_succeeded:
                  - align-self: center
                  - justify-self: end
                sb_total_backup_failed_label:
                  - align-self: center
                  - justify-self: start
                sb_total_backup_failed:
                  - align-self: center
                  - justify-self: end
            custom_fields:
              sb_status: >
                [[[ return `<ha-icon icon="mdi:folder-network" style="width:
                25px; height:
                25px;"></ha-icon><span>${entity.state}</span>`]]]   
              sb_Last_backup_label: |
                [[[ return `<span>Last Backup:</span>`]]]
              sb_Last_backup: >
                [[[ return '<span><b>' +
                states['sensor.samba_backup'].attributes.last_backup; +
                '</b></span>']]]
              sb_backup_local_label: |
                [[[ return '<span>Local Backups:<b></b></span>']]]
              sb_backup_local: >
                [[[ return '<span><b>' +
                states['sensor.samba_backup'].attributes.backups_local; +
                '</b></span>']]]
              sb_backup_remote_label: |
                [[[ return '<span>Backups Remote:</span>']]]
              sb_backup_remote: >
                [[[ return '<span><b>' +
                states['sensor.samba_backup'].attributes.backups_remote; +
                '</b></span>']]]
              sb_total_backup_succeeded_label: |
                [[[ return '<span>Total Backups Succeeded:</span>' ]]]
              sb_total_backup_succeeded: >
                [[[ return '<span><b>' +
                states['sensor.samba_backup'].attributes.total_backups_succeeded;
                + '</b></span>' ]]]
              sb_total_backup_failed_label: |
                [[[ return '<span>Total Backup Failed:</span>']]]
              sb_total_backup_failed: >
                [[[ return '<span><b>' +
                states['sensor.samba_backup'].attributes.total_backups_failed; +
                '</b></span>']]]
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_0
          - header_light
        name: Start Backup Now
        aspect_ratio: 2/.9
        entity: sensor.samba_backup
        icon: mdi:play
        show_state: false
        tap_action:
          action: call-service
          service: script.1647440573158
          data: {}
        state:
          - value: IDLE
            styles:
              card:
                - background-color: '#000044'
                - '--mdc-ripple-color': yellow
                - '--mdc-ripple-press-opacity': 0.5
                - font-size: 14px
              icon:
                - color: null
          - value: RUNNING
            styles:
              card:
                - background-color: '#000044'
                - '--mdc-ripple-color': yellow
                - '--mdc-ripple-press-opacity': 0.5
                - font-size: 14px
              icon:
                - color: lime
          - value: SUCCEEDED
            styles:
              card:
                - background-color: '#000044'
                - '--mdc-ripple-color': yellow
                - '--mdc-ripple-press-opacity': 0.5
                - font-size: 14px
              icon:
                - color: green
      - type: custom:button-card
        template:
          - header_0
          - header_light
        name: Reset All Counter
        aspect_ratio: 2/.9
        entity: null
        color: '#000044'
        icon: mdi:restart
        show_state: false
        tap_action:
          action: call-service
          service: script.001_samba_backup_reset_counter
          data: {}
        styles:
          card:
            - background-color: '#000044'
            - '--mdc-ripple-color': yellow
            - '--mdc-ripple-press-opacity': 0.5
            - font-size: 14px
  - type: custom:button-card
    color_type: blank-card
```

## Raspberry Pi 4

### Raspberry Pi 4 - View Image

![Raspberry](./images/Sk%C3%A6rmbillede%20fra%202023-01-05%2014-31-13.png)

### Raspberry Pi 4 - View yaml-code

```yaml
  - type: horizontal-stack
    cards:
      - type: custom:button-card
        template:
          - header_grid
        aspect_ratio: 1.8/1
        name: ''
        styles:
          grid:
            - grid-template-areas: >
                "label_n label_n" "label_0 text_0" "label_1 text_1" "label_2
                text_2" "label_3 text_3" "label_4 text_4" "label_5 text_5"
                "label_6 text_6"
            - grid-template-rows: 2fr 1fr 1fr  1fr 1fr 1fr 1fr 1fr
        custom_fields:
          label_0: >
            [[[ return '<ha-icon icon="mdi:thermometer" style="width: 15px;
            height: 15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                   states['sensor.processor_temperature'].attributes.friendly_name +
                  '</span>']]]
          label_1: >
            [[[ return '<ha-icon icon="mdi:fan" style="width: 15px; height:
            15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                states['sensor.argon_one_addon_fan_speed'].attributes.friendly_name; +
                '</span>']]]
          label_2: >
            [[[ return '<ha-icon icon="mdi:harddisk" style="width: 15px; height:
            15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                states['sensor.disk_use'].attributes.friendly_name; +
                '</span>']]]
          label_3: >
            [[[ return '<ha-icon icon="mdi:harddisk" style="width: 15px; height:
            15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                states['sensor.disk_free'].attributes.friendly_name; +
                '</span>']]]
          label_4: >
            [[[ return '<ha-icon icon="mdi:harddisk" style="width: 15px; height:
            15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                states['sensor.disk_use_percent'].attributes.friendly_name; +
                '</span>']]]
          label_5: >
            [[[ return '<ha-icon icon="mdi:cpu-32-bit" style="width: 15px;
            height: 15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                states['sensor.processor_use'].attributes.friendly_name; +
                '</span>']]]
          label_6: >
            [[[ return '<ha-icon icon="mdi:memory" style="width: 15px; height:
            15px;"></ha-icon>' + 
                  '<span>' + ' ' + 
                states['sensor.memory_free'].attributes.friendly_name; +
                '</span>']]]
          label_n: >
            [[[ return '<ha-icon icon="mdi:raspberry-pi"
            style="width:40px;"></ha-icon><span> Raspberry Pi 4</span>']]]
          text_0: |
            [[[ return '<span><b>' +
              states['sensor.processor_temperature'].state + 
              ' °C</b></span>' ]]]
          text_1: |
            [[[ return '<span><b>' +
              states['sensor.argon_one_addon_fan_speed'].state + 
              '</b></span>' ]]]
          text_2: |
            [[[ return '<span><b>' +
              states['sensor.disk_use'].state + 
              ' GiB</b></span>']]]
          text_3: |
            [[[ return '<span><b>' +
              states['sensor.disk_free'].state + 
              ' GiB</b></span>']]]
          text_4: |
            [[[ return '<span><b>' +
              states['sensor.disk_use_percent'].state + 
              ' %</b></span>']]]
          text_5: |
            [[[ return '<span><b>' +
              states['sensor.processor_use'].state + 
              ' %</b></span>']]]
          text_6: |
            [[[ return '<span><b>' +
              states['sensor.memory_free'].state + 
              ' MiB</b></span>']]]
```
