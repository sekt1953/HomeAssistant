# Her er min måde at instalerer Home Assistant

## Mit valg af udstyr

* [Raspberry Pi 4](https://raspberrypi.dk/produkt/raspberry-pi-4-model-b-8-gb/)
* [Argon ONE M.2 Case](https://raspberrypi.dk/produkt/argon-one-m-2-case-til-raspberry-pi-4/)
* Telegram for extern kommunitaion
* Zigbee til nogle forskellige føler og led lamper
  * SilverCrest
    * SilverCrest Zigbee Gateway, Model: **TYGWZ-01** solgt i LIDL
      * [Hacking the Silvercrest (Lidl) Smart Home Gateway](https://paulbanks.org/projects/lidl-zigbee/#overview "Paul Banks")
      * [Se hvordan du opdater](https://zigbee.blakadder.com/Lidl_TYGWZ-01.html "blakadder")
      * [Ny Software for opdatering](https://github.com/banksy-git/lidl-gateway-freedom "banksy-git")
    * [SilverCrest Outdoor Plug](https://zigbee.blakadder.com/Lidl_HG06619.html)
    * [SilverCrest Smart Plug DK Model HG06337-DK manufactured by Lidl Zigbee ID: TS011F | _TZ3000_upjrsxh1](https://zigbee.blakadder.com/Lidl_HG06337-DK.html)
    * [SilverCrest Doorbell Model HG06668 manufactured by Lidl Zigbee ID: TS0211 | _TZ1800_ladpngd](https://zigbee.blakadder.com/Lidl_HG06668.html)
    * [Silvercrest Radiator Valve Controller Model TVR01 manufactured by Lidl Zigbee ID: TS0601 | _TZE200_chyvmhay](https://zigbee.blakadder.com/Lidl_TVR01.html)
  * Sonoff
    * [Sonoff Motion Sensor, Model: SNZB-03 (timeout 2min)](https://www.proshop.dk/Smart-Home/Sonoff-SNZB-03-Motion-sensor/3084016?utm_source=pricerunner&utm_medium=cpc&utm_campaign=pricesite)
    * [Sonoff Zigbee Wireless Switch, Model: SNZB-01](https://www.proshop.dk/Smart-Home/Sonoff-Zigbee-Wireless-Switch/3084021?utm_source=pricerunner&utm_medium=cpc&utm_campaign=pricesite)
  * LIVARNO Smart Home (LIDL)
    * [Led Ceiling Light, Model-nr.: 14153706L / 14153806L](https://zigbee.blakadder.com/Lidl_14153706L.html)  
      * Nulstil lampen  
      For at forbinde lampen, skal den være i læringstilstanden. Dette vises ved et regelmæssigt blink af lampen.  
      Hvis lampen ikke blinker af sig selv, skal læringstilstanden nulstilles.   
      For at aktiverer læringstilstanden, skal du tænde og slukke lampen i følgende rytme:
        * tænd
        * 2 sek. slukket
        * 2 sec. tændt
        * 2 sek. slukket
        * 2 sec. tændt
        * 2 sek. slukket
        * 2 sec. tændt
    * [Smart Colour-Change LED Light Bulb IAN 360062_2010](https://zigbee.blakadder.com/Lidl_HG07834C.html)
    * [Livarno Lux E27 9W CCT Bulb](https://zigbee.blakadder.com/Lidl_HG06492C.html)
    * [LIDL Fjernbetjening TS1001 _TYZB01_bngwdjsr](https://zigbee.blakadder.com/Lidl_HG06323.html)
  * Ikea TRÅDFRI
    * E1810 TRÅDFRI fjernbetjening, 304.432.24
    * [E1745 TRÅDFRI bevægelsessensor, 704.299.13 (timeout 3min)](https://zigbee.blakadder.com/Ikea_E1745.html "zigbee.blakadder.com")
    * E27 TRÅDFRI LED 806lm, 704.391.58
  * Shelly
    * [Shelly Plus 1PM](https://www.proshop.dk/Smart-Home/Shelly-Plus-1PM/3027897?utm_source=pricerunner&utm_medium=cpc&utm_campaign=pricesite)
* ESP32 til egen fremstillet lysstyring via ESPHome
* Home Assistant OS, Supervised version

## 1. Argon One M.2 Case

* [Enable I2C](./Enable_I2C/README.md)
  * [Enable I2C with an SD card reader](./Enable_I2C/README.md#enable-i2c-with-an-sd-card-reader)
    * [Argon One Active Cooling & Argon One Active Linear Cooling Addon](./Enable_I2C/README.md#argon-one-active-cooling--argon-one-active-linear-cooling-addon)
  * [Enable I2C via Home Assistant Operating System Terminal](./Enable_I2C/README.md#enable-i2c-via-home-assistant-operating-system-terminal)
  * [the old way](https://github.com/mstedet/ESP32-2020#argon-one-m2---home-assistant-os-6x--supervised-version)

## 2. Installer Add-ons

### 2a. Installer Official Add-ons

* Studio Code Server
* MariaDB
  * Youtube videos [No More History Loss In Home Assistant!](https://www.youtube.com/watch?v=0Nf70avId0w "Smart Home Junkie")
  * Counfiguration
    * Logins
      * set password:
      * set username
    * Rights
      * database:
      * username:
* ESPHome
* File editor
  * Counfiguration
    * Directories First: on
    * Enforce Basepath: off
    * Git: off
* Samba share
  * Youtube videos [How to enable Samba in Home Assistant and access your files in your network](https://www.youtube.com/watch?v=udqY2CYzYGk "Smart Home Junkie")
  * Counfiguration
    * Username:
    * Password:
    * Workgroup: WORKGROUP
    * Enable Compatibility Mode: off
* SSH & Web Terminal
  * Youtube videos [Enable SSH In Home Assistant - TUTORIAL 2022](https://www.youtube.com/watch?v=_ANmn9QSLtA "Smart Home Junkie")
  * Counfiguration

### 2c. Installerer Home Assistant Community Store (HACS)

* Integrationer
  * HACS
    * youtube video [How to install HACS in 2022 in Home Assistant - NEW UPDATED VERSION!](https://www.youtube.com/watch?v=D6ZlhE-Iv9E "
Smart Home Junkie")
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
  * [](/Kode_Eksempler/DemoLysStyrimg.md)
* [Badeværelse](./Badev%C3%A6relse/README.md)
* [Køkken](./K%C3%B8kken/README.md)
  * [PWM-LightControler](./K%C3%B8kken/PWM-LightControler/)
    * [EspHome files:](./ESPHome/PWM-LightControler/) 
    * [FreeCAD files:](./FreeCAD/PWM-LightControler/)
    * [Fritzing files:](./Fritzing/PWM-LightControler/)

## 6. [Lovelace](./Lovelace/)

### Button-Card - Home, Kitchen, Server

I use [**custom-cards/button-card**](https://github.com/custom-cards/button-card) from **HACS** to design View's for **Home, Kitchen and Server**.  

* [Button-Card](./Lovelace/README.md#button-card)
  * [Intro](./Lovelace/README.md#intro)
  * [Source](./Lovelace/README.md#source)
  * [Images](./Lovelace/README.md#images)
  * [Subpage](./Lovelace/README.md#subpage)

## 10. ESPHome projecter

### USB -> Serial
* CH340
  * [Unable to use USB dongle based on USB-serial converter chip](https://unix.stackexchange.com/questions/670636/unable-to-use-usb-dongle-based-on-usb-serial-converter-chip)

* Min lysstyring
* ESP32-Cam 
* Klima Sensor
* Lys sensor
