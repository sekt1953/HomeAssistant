# ESPHome filer for pwm_kokken_old

```yaml
# Kilde til inspiration:
# ESP_Kode:
#   Youtube: https://www.youtube.com/watch?v=bEgpHPD2GaI&t=1623s
#   QuinLed: https://quinled.info/
# MOSFET PWM Driver:
#   Youtube: https://www.youtube.com/watch?v=GrvvkYTW_0k&t=303s
#   AddOhms: http://addohms.com/mosfet-introduction
# How to protect circuits from reversed voltage polarity!:
#   Afrotechmods:  https://www.youtube.com/watch?v=IrB-FPcv1Dc
#   Ralph S Bacon: https://www.youtube.com/watch?v=eS4_6XQi74c
# Issues on Connecting MOSFETs in Parallel
#   Lewis Loflin: https://www.youtube.com/watch?v=AOf-i2vLd2o
#Coolest motion detection sensor ever!
#   Youtube: https://www.youtube.com/watch?v=9-q2klKJ280
#   Youtube: https://www.youtube.com/watch?v=Hf19hc9PtcE&t=64s

substitutions:
  esphome_name: "pwm_kokken"
  esphome_frequency: "8000HZ"
  esphome_brightness: "50%"
  esphome_relative_brightness: "1%"
  esphome_transition_length: "0.1s"

esphome:
  name: ${esphome_name}
  platform: ESP32
  board: esp32dev

wifi:
  networks:
  - ssid: !secret My_WiFi_SSID
    password: !secret My_WiFi_Pass
  - ssid: !secret SEKT_WiFi_SSID
    password: !secret SEKT_WiFi_Pass
  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "${esphome_name} Fallback"
    password: !secret SEKT_AP_Pass

logger:
  level: debug
  #baud_rate: 0 #Disable logging/UART

api:
  password: !secret SEKT_API_Pass

ota:
  password: !secret SEKT_OTA_Pass

captive_portal:

# I2C for BME280 addr.: 0x76/0x77
i2c:
  sda: 21
  scl: 22
  scan: True
  id: bus_a

output:
  - platform: ledc
    pin: GPIO13
    frequency: ${esphome_frequency}
    id: LED_channel_1
  - platform: ledc
    pin: GPIO12
    frequency: ${esphome_frequency}
    id: LED_channel_2
  - platform: ledc
    pin: GPIO14
    frequency: ${esphome_frequency}
    id: LED_channel_3
  - platform: ledc
    pin: GPIO27
    frequency: ${esphome_frequency}
    id: LED_channel_4

light:
  - platform: monochromatic
    name: "${esphome_name}-1"
    default_transition_length: 3s
    output: LED_channel_1
    id: light_1
  - platform: monochromatic
    name: "${esphome_name}-2"
    default_transition_length: 3s
    output: LED_channel_2
    id: light_2
  - platform: monochromatic
    name: "${esphome_name}-3"
    default_transition_length: 3s
    output: LED_channel_3
    id: light_3
  - platform: monochromatic
    name: "${esphome_name}-4"
    default_transition_length: 3s
    output: LED_channel_4
    id: light_4

status_led:
  pin:
    number: GPIO2

sensor:
  - platform: uptime
    name: "${esphome_name}_Uptime Sensor"
    update_interval: 60s

  - platform: wifi_signal
    name: "${esphome_name}_WiFi Signal"
    update_interval: 60s

# BME280 Temperature, Pressure & Humidity
  - platform: bme280
    temperature:
      name: "${esphome_name}_BME280 Temperature"
      id: bme280_temperature
    pressure:
      name: "${esphome_name}_BME280 Pressure"
      accuracy_decimals: 0 
      id: bme280_pressure
    humidity:
      name: "${esphome_name}_BME280 Humidity"
      id: bme280_humidity
    address: 0x76
    update_interval: 30s

  - platform: template
    name: "${esphome_name}_Altitude"
    lambda: |-
      const float STANDARD_SEA_LEVEL_PRESSURE = 985.0; //in hPa, see note
      return ((id(bme280_temperature).state + 273.15) / 0.0065) *
        (powf((STANDARD_SEA_LEVEL_PRESSURE / id(bme280_pressure).state), 0.190234) - 1); // in meter
    update_interval: 60s
    icon: 'mdi:signal'
    unit_of_measurement: 'm'
  - platform: template
    name: "${esphome_name}_Equivalent sea level pressure"
    lambda: |-
      const float STANDARD_ALTITUDE = 69.0; // in meters, see note
      return id(bme280_pressure).state / powf(1 - ((0.0065 * STANDARD_ALTITUDE) /
        (id(bme280_temperature).state + (0.0065 * STANDARD_ALTITUDE) + 273.15)), 5.257); // in hPa
    update_interval: 60s
    accuracy_decimals: 2
    icon: 'mdi:gauge'
    unit_of_measurement: 'hPa'
  - platform: template
    name: "${esphome_name}_Absolute Humidity"
    lambda: |-
      const float mw = 18.01534;    // molar mass of water g/mol
      const float r = 8.31447215;   // Universal gas constant J/mol/K
      return (6.112 * powf(2.718281828, (17.67 * id(bme280_temperature).state) /
        (id(bme280_temperature).state + 243.5)) * id(bme280_humidity).state * mw) /
        ((273.15 + id(bme280_temperature).state) * r); // in grams/m^3
    accuracy_decimals: 2
    update_interval: 60s
    icon: 'mdi:water'
    unit_of_measurement: 'g/m³'
  - platform: template
    name: "${esphome_name}_Dew Point"
    lambda: |-
      return (243.5*(log(id(bme280_humidity).state/100)+((17.67*id(bme280_temperature).state) /
      (243.5+id(bme280_temperature).state)))/(17.67-log(id(bme280_humidity).state/100)-
      ((17.67*id(bme280_temperature).state)/(243.5+id(bme280_temperature).state))));
    unit_of_measurement: °C
    icon: 'mdi:thermometer-alert'

binary_sensor:
  - platform: gpio  # her tilsluttes f.eks. et pir mondul HC-SR501
    device_class: motion
    pin:
      number: GPIO15
      mode: INPUT_PULLDOWN
      inverted: False
    name: "${esphome_name}_Pir"

  - platform: gpio
    device_class: motion
    pin:
      number: GPIO4
      mode: INPUT_PULLDOWN
      inverted: False
    name: "${esphome_name}_Lys"
    id: bsensor_lys_1
    on_click:
    - min_length: 50ms
      max_length: 350ms
      then:
        - if:
            condition:
              api.connected
            then:
            - logger.log: connedted
            else:
              - logger.log: Not connedted
              - light.turn_on:
                  id: light_1
                  brightness: ${esphome_brightness}
              - light.turn_on:
                  id: light_2
                  brightness: ${esphome_brightness}
              - light.turn_on:
                  id: light_3
                  brightness: ${esphome_brightness}
              - light.turn_on:
                  id: light_4
                  brightness: ${esphome_brightness}
    - min_length: 500ms
      max_length: 1000ms
      then:
        - light.turn_on:
            id: light_1
            brightness: 0%
        - light.turn_on:
            id: light_2
            brightness: 0%
        - light.turn_on:
            id: light_3
            brightness: 0%
        - light.turn_on:
            id: light_4
            brightness: 0%
    on_press:
      then:
        - if:
            condition:
              api.connected
            then:
            - logger.log: connedted
            else:
              - logger.log: Not connedted
              - delay: 1s
              - while:
                  condition:
                    binary_sensor.is_on: bsensor_lys_1
                  then:
                  - light.dim_relative:
                      id: light_1
                      relative_brightness: ${esphome_relative_brightness}
                      transition_length: ${esphome_transition_length}
                  - light.dim_relative:
                      id: light_4
                      relative_brightness: ${esphome_relative_brightness}
                      transition_length: ${esphome_transition_length}
                  - delay: 0.1s

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
