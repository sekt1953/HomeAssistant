# Her er min måde at instalerer Home Assistant

## Mit valg af udstyr:
    * Raspberry Pi 4 
    * Argon ONE M.2 Case
    * Telegram for extern kommunitaion
    * Zigbee til nogle forskellige føler
    * ESP32 til egen fremstillet lysstyring via ESPHome
    * Home Assistant OS, Supervised version

# 1. Installation af Home Assistant OS, Supervised version i en Argon One M.2 Case
## [link til mstedet hvor jeg først skrev om dette](https://github.com/mstedet/ESP32-2020#argon-one-m2---home-assistant-os-6x--supervised-version)

    * Opdaterer RPI Firmware til nyeste
    * Boot RPI fra M.2 disk
    * Installer Home Assistant OS, Supervised version
    * Enable I2C 
    * Installer Argon One active cooling

# 2. Installer Add-ons
## 2a. Installer Official Add-ons
    * File editor
    * Samba share
    * MariaDB
      * System Monitering
   
## 2b. Installer Home Assistant Community Add-ons
    * ESPHome
    * motionEye
    * Visual Studio Code
    * SSH & Web Terminal

## 2c. Installerer Home Assistant Community Store (HACS)
    * Integrationer
      * HACS
      * Waste Collection Schedule
    * Frontend
      * Light Entity Row
      * simple-clock-card
      * slider-entity-row

# 3. Telegram, hvordan instalerer jeg Telegram Bot med polling & notification
    * hvordan finder jeg bruger chat_id
    * hvordan finder jeg group chat_id

# 4. Zigbee
    * CC2531, hvordan opdataren jeg firmware 
    * LIDL Zigbee gateway (Silvercrest  Smart Home Gateway)
## Flashing CC2531 without CC Debugger
[Følg denne denne vejledning](https://notenoughtech.com/home-automation/flashing-cc2531-without-cc-debugger/), jeg brugte 4 [Dupont Kabel M-F 20cm](https://ardustore.dk/produkt/dupont-breadboard-kabel), jeg lodede Male enden på connector bennene og Female enden forbandt jeg til RaspberryPi'en, USB stikket blev også forbundet til RaspberryPi'en.
## Flashing SilverCrest Zigbee Gateway
[Følg denne vejledning](https://zigbee.blakadder.com/Lidl_TYGWZ-01.html)

# 4. Mine Automationer & Script mm.. 

# 10. ESPHome projecter
    * Min lysstyring
    * ESP32-Cam 
    * Klima Sensor
    * Lys sensor
