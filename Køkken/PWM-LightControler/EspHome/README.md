# ESPHome filer for pwm_kokken_new

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
  esphome_name: "pwm_kokken_new"
  esphome_frequency: "8000HZ"
  esphome_brightness: "50%"
  esphome_relative_brightness: "1%"
  esphome_transition_length: "0.1s"
  glyphs_ssd1306: "!%()+=,-_.:€°/0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZÆØÅ abcdefghijklmnopqrstuvwxyzæøå"

esphome:
  name: ${esphome_name}
  platform: ESP32
  board: esp32dev

wifi:
  networks:
  - ssid: !secret WiFi_SSID
    password: !secret WiFi_Pass

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
    size: 14
    glyphs: $glyphs_ssd1306

  - file: './ttf/DejaVuSerif.ttf'
    id: font4
    size: 12
    glyphs: $glyphs_ssd1306

display:
  - platform: ssd1306_i2c
    model: "SH1106 128x64"
    address: 0x3C
    lambda: |-
      // Print "Mitt Smarta Hus" in top center.
      //it.printf(64, 0, id(font4), TextAlign::TOP_CENTER, "Mit Smarte Hjem");

      it.printf(0, 0, id(font4), TextAlign::TOP_LEFT, "%s", id(kok_display).state.c_str());
      it.printf(127, 23, id(font4), TextAlign::TOP_RIGHT, "%s", id(kok_display).state.c_str());
      
      // Print time in HH:MM format
      // it.strftime(0, 60, id(font2), TextAlign::BASELINE_LEFT, "%H:%M", id(esptime).now());

      // Print inside temperature (from homeassistant sensor)
      if (id(box_temperature).has_state()) {
        it.printf(127, 46, id(font3), TextAlign::TOP_RIGHT , "%.1f°", id(box_temperature).state);
      }
      
      // Print outside temperature (from homeassistant sensor)
      //it.printf(127, 60, id(font4), TextAlign::BASELINE_RIGHT ,  "abc");
      

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
  - platform: ledc
    pin: GPIO26
    frequency: ${esphome_frequency}
    id: LED_channel_5
  - platform: ledc
    pin: GPIO25
    frequency: ${esphome_frequency}
    id: LED_channel_6

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
  - platform: monochromatic
    name: "${esphome_name}-5"
    default_transition_length: 3s
    output: LED_channel_5
    id: light_5
  - platform: monochromatic
    name: "${esphome_name}-6"
    default_transition_length: 3s
    output: LED_channel_6
    id: light_6

#status_led:
#  pin:
#    number: GPIO2

dallas:
  - pin: 23


sensor:
  - platform: uptime
    name: "${esphome_name}_Uptime Sensor"
    update_interval: 60s

  - platform: wifi_signal
    name: "${esphome_name}_WiFi Signal"
    update_interval: 60s

  - platform: dallas  # Dallas DS18b20
    address: 0x060316b55a71ff28
    name: "${esphome_name}_temp"
    
  - platform: homeassistant
    id: box_temperature
    entity_id: sensor.pwm_kokken_new_temp
    internal: true

# BME280 Temperature, Pressure & Humidity
  - platform: bme280
    temperature:
      name: "${esphome_name}_BME280 Temperature"
      id: bme280_temperature
      accuracy_decimals: 2
      oversampling: 16x
    pressure:
      name: "${esphome_name}_BME280 Pressure"
      id: bme280_pressure
      accuracy_decimals: 2
    humidity:
      name: "${esphome_name}_BME280 Humidity"
      id: bme280_humidity
    address: 0x76
    iir_filter: 16x
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
  - platform: homeassistant
    id: kok_display
    entity_id: input_text.kitchen_display_friendly_name
    name: "Display_text"
```