# Lovelace

## Kitchen Timer with Button-Card

* Kilde: 
  * https://github.com/custom-cards/button-card
  * [Community guides:](https://github.com/custom-cards/button-card#community-guides)
    * https://robotnet.dk/2020/homekit-knapper-custom-buttons-home-assistant.html
  * [Credits](https://github.com/custom-cards/button-card#credits)
  * CSS Grid
    * [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
    * [CSS Grid Course](https://www.youtube.com/watch?v=t6CBKf8K_Ac)
      * [Learn CSS Grid for free](https://scrimba.com/learn/cssgrid)

|Home|Kitchen-Timer|Samba-Backup|
| :---: | :---: | :---: |
|![](./button-card/images/Sk%C3%A6rmbillede%20fra%202023-01-02%2023-51-28.png)  |![Kitchen Timer](./button-card/images/Sk%C3%A6rmbillede%20fra%202022-12-29%2023-31-09.png)|![Samba-backup](./button-card/images/Sk%C3%A6rmbillede%20fra%202023-01-04%2002-54-03.png)|

* Templates
  * [Button Card Templates](./button-card/ButtonCardTemplates.md)
* Home
  * [View](./button-card/Home.md)
    * [Clock](./button-card/Home.md#clock)
    * [Light](./button-card/Home.md#light)
* Kitchen
  * View
    * [Clomplet Raw KitchenTimerView.yaml](./button-card/Raw/KitchenTimerView.yaml)
    * [Clock](./button-card/KitchenTimerview.md#clock)
    * [Timer](./button-card/KitchenTimerview.md#timer)
    * [Light](./button-card/KitchenTimerview.md#light)
  * Helpers
    * [kitchens.yaml](./button-card/KitchensTimerYaml.md)
  * Script
    * [Timer Start](./button-card/KitchenTimerStart.md)
  * [Telegram Notify](./button-card/KitchenTelegramNotify.md)
    * [Configuration - /config/configuration.yaml](./button-card/KitchenTelegramNotify.md#configuration)
    * [Automations - KitchenTimerChangeState](./button-card/KitchenTelegramNotify.md#automations)
* [Server](./button-card/ServerSambaBackup.md#server)
  * [Clock](./button-card/ServerSambaBackup.md#clock)
  * [Samba-Backup](./button-card/ServerSambaBackup.md#samba-backup)
  * [Raspberry Pi 4](./button-card/ServerSambaBackup.md#raspberry-pi-4)
