# Her er min måde at instalerer Home Assistant

## Mit valg af udstyr

* [Raspberry Pi 4](https://raspberrypi.dk/produkt/raspberry-pi-4-model-b-8-gb/)
* [Argon ONE M.2 Case](https://raspberrypi.dk/produkt/argon-one-m-2-case-til-raspberry-pi-4/)
* Telegram for extern kommunitaion
* Zigbee til nogle forskellige føler og led lamper
  * SilverCrest Zigbee Gateway, Model: **TYGWZ-01** solgt i LIDL
    * [Se hvordan du opdater](https://zigbee.blakadder.com/Lidl_TYGWZ-01.html)
  * [Sonoff Motion Sensor, Model: SNZB-03](https://www.proshop.dk/Smart-Home/Sonoff-SNZB-03-Motion-sensor/3084016?utm_source=pricerunner&utm_medium=cpc&utm_campaign=pricesite)
  * [Sonoff Zigbee Wireless Switch, Model: SNZB-01](https://www.proshop.dk/Smart-Home/Sonoff-Zigbee-Wireless-Switch/3084021?utm_source=pricerunner&utm_medium=cpc&utm_campaign=pricesite)
  * LIVARNO Smart Home
    * [Led Ceiling Light, Model-nr.: 14153706L / 14153806L](https://zigbee.blakadder.com/Lidl_14153706L.html)
    * [Smart Colour-Change LED Light Bulb IAN 360062_2010](https://zigbee.blakadder.com/Lidl_HG07834C.html)
    * [Livarno Lux E27 9W CCT Bulb](https://zigbee.blakadder.com/Lidl_HG06492C.html)
    * [LIDL Fjernbetjening TS1001 _TYZB01_bngwdjsr](https://zigbee.blakadder.com/Lidl_HG06323.html)
  * SilverCrest
    * [SilverCrest Outdoor Plug](https://zigbee.blakadder.com/Lidl_HG06619.html)
  * Ikea TRÅDFRI
    * E1810 TRÅDFRI fjernbetjening, 304.432.24
    * E1745 TRÅDFRI bevægelsessensor, 704.299.13 (fejlkøb)
    * E27 TRÅDFRI LED 806lm, 704.391.58
  * Shelly
    * [Shelly Plus 1PM](https://www.proshop.dk/Smart-Home/Shelly-Plus-1PM/3027897?utm_source=pricerunner&utm_medium=cpc&utm_campaign=pricesite)
* ESP32 til egen fremstillet lysstyring via ESPHome
* Home Assistant OS, Supervised version

## 1. Installation af Home Assistant OS, Supervised version i en Argon One M.2 Case

### [link til mstedet hvor jeg først skrev om dette](https://github.com/mstedet/ESP32-2020#argon-one-m2---home-assistant-os-6x--supervised-version)

* Opdaterer RPI Firmware til nyeste
* Boot RPI fra M.2 disk
* Installer Home Assistant OS, Supervised version
* [Enable I2C](./Enable_I2C/README.md)
* Installer Argon One active cooling

## 2. Installer Add-ons

### 2a. Installer Official Add-ons

* File editor
* Samba share
* MariaDB
  * System Monitering

### 2b. Installer Home Assistant Community Add-ons

* ESPHome
* motionEye
* Visual Studio Code
* SSH & Web Terminal

### 2c. Installerer Home Assistant Community Store (HACS)

* Integrationer
  * HACS
  * Waste Collection Schedule
* Frontend
  * Light Entity Row
  * simple-clock-card
  * slider-entity-row

## 3. Telegram, hvordan instalerer jeg Telegram Bot med polling & notification

* hvordan finder jeg bruger chat_id
* hvordan finder jeg group chat_id

## 4. Zigbee gateway flashing

Jeg har to typer af Zigbee Gateway, i min gamle opsætning brugte jeg 

* CC2531, hvordan opdataren jeg firmware
  * [Flashing CC2531 without CC Debugger](./Flashing_CC2531/README.md)

I min nye installation har jeg valgt at bruge denne gateway fra LIDL

* LIDL Zigbee gateway (Silvercrest  Smart Home Gateway)
  * [Flashing SilverCrest Zigbee Gateway](./Flashing_SilverCrest/README.md)

## 5. Mine Automationer & Script mm

* [Kode eksempler](./Kode_Eksempler/)
  * [Sonoff **SNZB-01**, med brug af **zha_event**](./Kode_Eksempler/Sonoff_SNZB-01.md)
* [Badeværelse](./Badev%C3%A6relse/README.md)
* [Køkken](./K%C3%B8kken/README.md)
  * [PWM-LightControler](./K%C3%B8kken/PWM-LightControler/)
    * [EspHome](./K%C3%B8kken/PWM-LightControler/EspHome/)
    * [FreeCAD](./K%C3%B8kken/PWM-LightControler/FreeCAD/)
    * [Fritzing](./K%C3%B8kken/PWM-LightControler/Fritzing/)

## 10. ESPHome projecter

* Min lysstyring
* ESP32-Cam 
* Klima Sensor
* Lys sensor
