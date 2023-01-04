# Lovelace

## Button-Card

### Intro

I use [**custom-cards/button-card**](https://github.com/custom-cards/button-card) from **HACS** to design View's for **Home, Kitchen and Server**.  

* Home View:
  * In **Home View**, I have an overview of my Light-settings and Motion-Sensor, and can set most of the light from there.
  * My light switches will have 3 functions:
    * [**tap_action**](https://github.com/custom-cards/button-card#main-options): which toggles light on/off.
    * [**double_tap_action**](https://github.com/custom-cards/button-card#main-options): which toggles light between High/Low (50% / 12%) brightness.
    * [**hold_action**](https://github.com/custom-cards/button-card#main-options): which toggles between Day/Night-light (white 12% / red 1%).
* Kitchen:
* Server:
  * For my design of the **Server View**, I have used [**ADVANCED styling options**](https://github.com/custom-cards/button-card#advanced-styling-options) and got a lot of help from the page [**A Complete Guide to CSS Grid**](https://css-tricks.com/snippets/css/complete-guide-grid/), a slightly messy page, but full of good information.

### Source

* https://github.com/custom-cards/button-card
* [Community guides:](https://github.com/custom-cards/button-card#community-guides)
  * https://robotnet.dk/2020/homekit-knapper-custom-buttons-home-assistant.html
* [Credits](https://github.com/custom-cards/button-card#credits)
* CSS Grid
  * [A Complete Guide to CSS Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
  * [CSS Grid Course](https://www.youtube.com/watch?v=t6CBKf8K_Ac)
    * [Learn CSS Grid for free](https://scrimba.com/learn/cssgrid)

### Images

|Home|Kitchen|Server|
|:---:|:---:|:---:|
|![Home](./button-card/images/Sk%C3%A6rmbillede%20fra%202023-01-02%2023-51-28.png)  |![Kitchen Timer](./button-card/images/Sk%C3%A6rmbillede%20fra%202022-12-29%2023-31-09.png)|![Samba-backup](./button-card/images/Sk%C3%A6rmbillede%20fra%202023-01-04%2002-54-03.png)|

### Subpage

* Templates
  * [Button Card Templates](./button-card/ButtonCardTemplates.md)
* [Home](./button-card/Home.md)
  * [Clock](./button-card/Home.md#clock)
  * [Light](./button-card/Home.md#light)
* [Kitchen](./button-card/KitchenTimerStart.md)
  * View
    * [Clock](./button-card/KitchenTimerview.md#clock)
    * [Timer](./button-card/KitchenTimerview.md#timer)
    * [Light](./button-card/KitchenTimerview.md#light)
  * Helpers
    * [Timers](./button-card/KitchensTimerYaml.md)
  * Script
    * [Timer Start](./button-card/KitchenTimerStart.md)
  * [Telegram Notify](./button-card/KitchenTelegramNotify.md)
    * [Configuration - /config/configuration.yaml](./button-card/KitchenTelegramNotify.md#configuration)
    * [Automations - KitchenTimerChangeState](./button-card/KitchenTelegramNotify.md#automations)
* [Server](./button-card/ServerSambaBackup.md#server)
  * [Clock](./button-card/ServerSambaBackup.md#clock)
  * [Samba-Backup](./button-card/ServerSambaBackup.md#samba-backup)
  * [Raspberry Pi 4](./button-card/ServerSambaBackup.md#raspberry-pi-4)
