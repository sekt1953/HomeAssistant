# Her er min måde at instalerer Home Assistant

## Mit valg af udstyr

    * Raspberry Pi 4 
    * Argon ONE M.2 Case
    * Telegram for extern kommunitaion
    * Zigbee til nogle forskellige føler
    * ESP32 til egen fremstillet lysstyring via ESPHome
    * Home Assistant OS, Supervised version

## 1. Installation af Home Assistant OS, Supervised version i en Argon One M.2 Case

### [link til mstedet hvor jeg først skrev om dette](https://github.com/mstedet/ESP32-2020#argon-one-m2---home-assistant-os-6x--supervised-version)

    * Opdaterer RPI Firmware til nyeste
    * Boot RPI fra M.2 disk
    * Installer Home Assistant OS, Supervised version
    * Enable I2C 
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

    * CC2531, hvordan opdataren jeg firmware 
    * LIDL Zigbee gateway (Silvercrest  Smart Home Gateway)

### Flashing CC2531 without CC Debugger

[Følg denne vejledning](https://notenoughtech.com/home-automation/flashing-cc2531-without-cc-debugger/), jeg brugte 4 [Dupont Kabel M-F 20cm](https://ardustore.dk/produkt/dupont-breadboard-kabel), jeg lodede Male enden på connector bennene og Female enden forbandt jeg til RaspberryPi'en, USB stikket blev også forbundet til RaspberryPi'en.

#### Kabel tabel

| Raspberry Pin | Raspberry Name  | CC2531 |
|:---:          |:---:            |:---:   |
| GND           | GND             | GND    |
| Pin 38        | BCM 20          | DD     |
| Pin 36        | BCM 16          | DC     |
| Pin 35        | BCM 19          | RST    |

### Flashing SilverCrest Zigbee Gateway

I første del af vejlingen som jeg linker til er der et afsnit "Retrieve Root Password", her valgte jeg at monterer 3 stk dupoint connector til at forbindelse til TTL-adapteren, de kan blive efter opsætningen, så er de der hvis der kommer nyt software.

| Gateway    | TTL-adapteren |
|:---:       |:---:          |
| Serial TX  | RX            |
| Serial RX  | TX            |
| GND        | GND           |

### !! Husk at Serial til TTL adapteren skal være sat til 3,3V

#### Serial Terminal

Serial_adapteren skal snakke med en tty terminal, her har jeg valgt at bruge Putty for Linux. Med Putty er det nemt at sætte de rigtiǵe indstillinger for samtalen, her er mine valg:

```txt
Settings: 
    Windows -> Font -> Font used for ordinary text ->
        Client: Ubuntu Mono 16
    Connection -> Serial ->
        Serial line to connect to: /dev/ttyUSB0
    Configure teh serial line ->
        Speed:          38400
        Data bits:      8
        Stop bits:      1
        Parity:         None
        Flow control:   None
    Session ->
        Saved session:  LidlGateway     
```

### Decryptering

For at kunne få held med decryptering, skal der instaleres lidt hjælpe værktøjer på min Linux PC, [vejledning fundet her:](https://stackoverflow.com/questions/11596839/installing-pycrypto-on-ubuntu-fatal-error-on-build),
 komandoerne vist herunder:

```code
sudo apt-get install python3.8-dev
pip install pycrypto
```

For resten af vejen [følg denne vejledning](https://zigbee.blakadder.com/Lidl_TYGWZ-01.html), god fornøjelse.

## 5. Mine Automationer & Script mm

### [Badeværelse](./Badev%C3%A6relse/README.md) 

## 10. ESPHome projecter

    * Min lysstyring
    * ESP32-Cam 
    * Klima Sensor
    * Lys sensor
