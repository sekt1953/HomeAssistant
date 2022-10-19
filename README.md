# Her er min måde at instalerer Home Assistant

## Mit valg af udstyr

* [Raspberry Pi 4](https://raspberrypi.dk/produkt/raspberry-pi-4-model-b-8-gb/)
* [Argon ONE M.2 Case](https://raspberrypi.dk/produkt/argon-one-m-2-case-til-raspberry-pi-4/)
* Telegram for extern kommunitaion
* Zigbee til nogle forskellige føler og led lamper
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

* [Badeværelse](./Badev%C3%A6relse/README.md)

## 10. ESPHome projecter

* Min lysstyring
* ESP32-Cam 
* Klima Sensor
* Lys sensor
