# Kursus 2022-11-29

## Lovelace

![](./Images/Sk%C3%A6rmbillede%20fra%202022-11-28%2022-16-17.png)

Her er Lovelace koden i yaml:

```yaml
square: false
columns: 1
type: grid
cards:
  - type: entities
    entities:
      - entity: sensor.solvarme_top_temperature
      - entity: sensor.solvarme_bund_temperature
      - entity: binary_sensor.solvarme_touch_pad_15
    title: Solvarme Tank
  - type: entities
    entities:
      - entity: sensor.klima280_bme280_temperature
        name: BME280 Temperature
      - entity: sensor.klima280_bme280_humidity
        name: BME280 Humidity
      - entity: sensor.klima280_bme280_pressure
        name: BME280 Pressure
      - entity: sensor.klima280_bh1750_illuminance
        name: BH1750 Illuminance
    title: Klima
```

## ESPHome Kode

### Solvarme tank

Her har vi en ESP32 med
 * 2 stk. [DS18B20 1-Wire Temperature Sensor](https://esphome.io/components/sensor/dallas.html?highlight=ds18b20)
 * 1 stk. [SSD1306 OLED Display](https://esphome.io/components/display/ssd1306.html)

Her er ESPHome YAML coden:

```yaml
substitutions:
  esphome_name: "solvarme"
  esphome_status_led: GPIO2
  esphome_dalas_pin: GPIO19 
  glyphs_ssd1306: "!%()+=,-_.:€°/0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZÆØÅ abcdefghijklmnopqrstuvwxyzæøå"

esphome:
  name: ${esphome_name}
  platform: ESP32
  board: esp32dev

wifi:
  networks:
  - ssid: TP-Link_36A0
    password: 02485515

  ap:
    # Enable fallback hotspot (captive portal) in case wifi connection fails
    ssid: "${esphome_name} Fallback"
    password: !secret AP_Pass

logger:
  level: debug
  #baud_rate: 0 #Disable logging/UART

api:
  password: !secret API_Pass

ota:
  password: !secret OTA_Pass

captive_portal:

time:  # Get the time from Home Assistant to sync the onboard real-time clock.
  - platform: homeassistant
    id: esptime

font:
  - file: './ttf/slkscr.ttf'
    id: font1
    size: 8
    glyphs: $glyphs_ssd1306

  - file: './ttf/BebasNeue-Regular.ttf'
    id: font2
    size: 48

  - file: './ttf/Arial.ttf'
    id: font3
    size: 24
    glyphs: $glyphs_ssd1306

  - file: './ttf/DejaVuSerif.ttf'
    id: font4
    size: 12
    glyphs: $glyphs_ssd1306

display:
  - platform: ssd1306_i2c
    model: "SH1106 128x64"
    rotation: 270
    address: 0x3C
    lambda: |-
      // Print "Mitt Smarta Hus" in top center.
      //it.printf(64, 0, id(font4), TextAlign::TOP_CENTER, "Mit Smarte Hjem");
      
      // Print temperature (from homeassistant sensor)
      if (id(${esphome_name}_Top_Temperature).has_state()) {
        it.printf(32, 24, id(font3), TextAlign::BASELINE_CENTER , "%.1f°", id(${esphome_name}_Top_Temperature).state);
      }

      // Print time in HH:MM format
      it.strftime(32, 70, id(font3), TextAlign::BASELINE_CENTER, "%H:%M", id(esptime).now());

      // Print inside temperature (from homeassistant sensor)
      if (id(${esphome_name}_Bund_Temperature).has_state()) {
        it.printf(32, 120, id(font3), TextAlign::BASELINE_CENTER , "%.1f°", id(${esphome_name}_Bund_Temperature).state);
      }

      
# I2C for BME280 addr.: 0x76/0x77
i2c:
  sda: 21
  scl: 22
  scan: True
  id: bus_a
#status_led:
#  pin:
#    number: ${esphome_status_led}


dallas:
  - pin: ${esphome_dalas_pin}
    update_interval: 60s

esp32_touch:
  setup_mode: False

binary_sensor:
  - platform: esp32_touch
    name: "${esphome_name}_Touch_Pad_15"
    pin: GPIO15
    threshold: 500
    id: ${esphome_name}_Touch_Pad_15

sensor:
  - platform: dallas
    address: 0x64000006B629FD28
    #index: 0
    resolution: 12
    accuracy_decimals: 2
    name: "${esphome_name}_Top_Temperature"
    id: ${esphome_name}_Top_Temperature

  - platform: dallas
    address: 0xe93c33f649ed7e28
    #index: 0
    resolution: 12
    accuracy_decimals: 2
    name: "${esphome_name}_Bund_Temperature"
    id: ${esphome_name}_Bund_Temperature

  - platform: uptime
    name: "${esphome_name}_Uptime Sensor"
    update_interval: 60s

  - platform: wifi_signal
    name: "${esphome_name}_WiFi Signal"
    update_interval: 60s

text_sensor:
  - platform: wifi_info
    ip_address:
      name: "${esphome_name}_IP Address"
    ssid:
      name: "${esphome_name}_Connected SSID"
    bssid:
      name: "${esphome_name}_Connected BSSID"
    mac_address:
      name: "${esphome_name}_Mac Wifi Address"
  - platform: version
    name: "${esphome_name}_ESPHome version"
```

### Klima

Her har vi en ESP32 med 
 * [BME280 Temperature, Pressure & Humidity Sensor. ](https://esphome.io/components/sensor/bme280.html)
 * [BH1750 Ambient Light Sensor.](https://esphome.io/components/sensor/bh1750.html?highlight=bh1750)

Her er ESPHome YAML coden:

```yaml
substitutions:
  esphome_name: "klima280"

esphome:
  name: ${esphome_name}

esp32:
  board: esp32dev
  framework:
    type: arduino

# Enable logging
logger:

# Enable Home Assistant API
api:
  encryption:
    key: "RBA3T4yihkYwSpq7Om9Xxqgz9kuplCJ2V3z9A0HFEjQ="

ota:
  password: "146d68b1590a860a68fc2fafb96d2d8a"

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Klima280 Fallback Hotspot"
    password: "XRVvEQBGg8Q4"

captive_portal:

time:  # Get the time from Home Assistant to sync the onboard real-time clock.
  - platform: homeassistant
    id: esptime    

# I2C for BME280 addr.: 0x76/0x77
i2c:
  sda: 21
  scl: 22
  scan: True
  id: bus_a

sensor:
  - platform: bme280
    temperature:
      name: "${esphome_name} BME280 Temperature"
      oversampling: 16x
    pressure:
      name: "${esphome_name} BME280 Pressure"
    humidity:
      name: "${esphome_name} BME280 Humidity"
    address: 0x76
    update_interval: 60s

  - platform: bh1750
    name: "${esphome_name} BH1750 Illuminance"
    address: 0x23
    update_interval: 60s

```