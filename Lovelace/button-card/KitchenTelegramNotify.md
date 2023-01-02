# Telegram Notify

## New Server ha-8-sekt

### Configuration

/config/configuration.yaml

```yaml
[...]

# Telegram
telegram_bot:
  - platform: polling
    api_key: !secret telegram_api_token
    allowed_chat_ids:
      - !secret telegram_chat_id_user1
      - !secret telegram_chat_id_group1

notify:
  - platform: telegram
    name: !secret telegram_NOTIFIER_User1
    chat_id: !secret telegram_chat_id_user1

  - platform: telegram
    name: !secret telegram_NOTIFIER_group1
    chat_id: !secret telegram_chat_id_group1

[...]
```

## Automations

### Automation: KitchenTimerChangeState

```yaml
alias: KitchenTimerChangeState
description: ""
trigger:
  - platform: state
    entity_id:
      - timer.kitchen_001_aeg_blodkogte
      - timer.kitchen_002_aeg_hardkogte
      - timer.kitchen_003_rugbrod_haevetid
      - timer.kitchen_004_rugbrod_bagetid
      - timer.kitchen_005_fodselsdagsboller_haevetid_1
      - timer.kitchen_006_fodselsdagsboller_haevetid_2
      - timer.kitchen_007_fodselsdagsboller_bagetid
      - timer.kitchen_008_grahamsbrod_haevetid
      - timer.kitchen_009_grahamsbrod_bagetid
      - timer.kitchen_010_morgen_boller_bagetid
    from: active
    to: idle
condition: []
action:
  - service: notify.persistent_notification
    data:
      message: "{{ trigger.to_state.name }}"
      title: "Køkken Timer Slut !! "
  - service: notify.sekt1953_group_1
    data:
      title: "Køkken Timer Slut !! "
      message: "{{ trigger.to_state.name }}"
mode: queued
max: 10
```
