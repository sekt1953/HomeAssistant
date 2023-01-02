# Server 

## Samba-Backup

### Intro

For my design of the **samba backup view**, I have used [ADVANCED styling options](https://github.com/custom-cards/button-card#advanced-styling-options) and got a lot of help from the page [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/), a slightly messy page, but full of good information.  
As on my other pages, I always have a clock at the top, so you always have easy access to the time. As a clock I use a **HACS Frontend simple-clock-card**

### Samba-Backup View images

![Samba-Backup](./images/Sk%C3%A6rmbillede%20fra%202023-01-02%2017-44-45.png)

### Samba-Backup View yaml-code

```yaml
type: vertical-stack
cards:
  - type: custom:simple-clock-card
    use_military: true
    hide_seconds: true
  - type: horizontal-stack
    cards:
      - type: vertical-stack
        cards:
          - type: custom:button-card
            entity: sensor.samba_backup
            icon: mdi:upload-network
            aspect_ratio: 2/1
            name: Samba Backup
            styles:
              card:
                - background-color: '#000044'
                - border-radius: 1%
                - padding: 5%
                - color: ivory
                - font-size: 15px
                - text-shadow: 0px 0px 5px black
                - text-transform: capitalize
              grid:
                - grid-template-areas: >-
                    "n sb_status"    
                    "sb_Last_backup sb_Last_backup"
                    "sb_backup_local sb_backup_local"  
                    "sb_backup_remote sb_backup_remote" 
                    "sb_total_backup_succeeded sb_total_backup_succeeded" 
                    "sb_total_backup_failed sb_total_backup_failed"
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
                sb_Last_backup:
                  - align-self: center
                  - justify-self: start
                sb_backup_local:
                  - align-self: center
                  - justify-self: start
                sb_backup_remote:
                  - align-self: center
                  - justify-self: start
                sb_total_backup_succeeded:
                  - align-self: center
                  - justify-self: start
                sb_total_backup_failed:
                  - align-self: center
                  - justify-self: start
            custom_fields:
              sb_status: >
                [[[ return `<ha-icon icon="mdi:upload-network" style="width:
                25px; height: 25px;
                "></ha-icon><span>${entity.state}</span>`]]]   
              sb_Last_backup: >
                [[[ return '<span>Last Backup:<b>' +
                states['sensor.samba_backup'].attributes.last_backup; +
                '</b></span>']]]
              sb_backup_local: >
                [[[ return '<span>Backups Local:<b>' +
                states['sensor.samba_backup'].attributes.backups_local; +
                '</b></span>']]]
              sb_backup_remote: >
                [[[ return '<span>Backups Remote:<b>' +
                states['sensor.samba_backup'].attributes.backups_remote; +
                '</b></span>']]]
              sb_total_backup_succeeded: >
                [[[ return '<span>Total Backups Succeeded:<b>' +
                states['sensor.samba_backup'].attributes.total_backups_succeeded;
                + '</b></span>' ]]]
              sb_total_backup_failed: >
                [[[ return '<span>Total Backup Failed:<b>' +
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
```

## Raspberry Pi 4

### Raspberry Pi 4 View Image

### Raspberry Pi 4 View yaml-code

```yaml

```