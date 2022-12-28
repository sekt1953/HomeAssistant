# Telegram Notify

## New Server ha-8-sekt

Configuration:

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

## Old Server

Automation: 04_egg_and_Backing_timer

```yaml
alias: 04_egg_and_Backing_timer
trigger:
  - platform: state
    entity_id:
      - timer.aeg_blodkogte
      - timer.aeg_hardkogte
      - timer.fodselsdagsboller_haevetid_1
      - timer.fodselsdagsboller_haevetid_2
      - timer.fodselsdagsboller_bagetid
      - timer.morgen_bollere_bagetid
      - timer.rugbrod_haevetid
      - timer.rugbrod_bagetid
      - timer.svendbrodet_haevetid_1
      - timer.svendbrodet_haevetid_2
      - timer.svendbrodet_bagetid
      - timer.svendboller
      - timer.grahamsbrod_haevetid
      - timer.grahamsbrod_bagetid
    from: active
    to: idle
condition: []
action:
  - service: notify.persistent_notification
    data:
      title: "Køkken Timer Slut !! "
      message: "{{ trigger.to_state.name }}"
  - service: notify.sekt1953_group_1
    data:
      title: "Køkken Timer Slut !! "
      message: "{{ trigger.to_state.name }}"
mode: single

```

Configuration:

```yaml
# Example configuration.yaml entry for the Telegram Bot
telegram_bot:
  - platform: polling   # 202012172116 @sekt1953_1_bot
    api_key: !secret telegram_api_key
    allowed_chat_ids:
      - 837103786        # username: sekt1953
      - -1001361577327   # title: sekt1953_group_1, type: supergroup
      - -1001717170907   # title: Hassio-2021, type: supergroup
```

Comment:

```yaml
- 837103786        # first_name: Svenn-Erik K.,last_name: Thomsen, username: sekt1953 (https://t.me/sekt1953), language_code: da (-),  created: newer than 7/2019 (?) (https://t.me/getidsbot?start=idhelp)
```