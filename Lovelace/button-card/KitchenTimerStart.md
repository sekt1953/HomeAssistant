# Script

## TimerStart

```yaml
alias: TimerStart
sequence:
  - if:
      - condition: template
        value_template: "{{ is_state(thetimer,'idle')}}"
    then:
      - service: timer.start
        data: {}
        target:
          entity_id: "{{thetimer}}"
mode: single
icon: mdi:timer
```
