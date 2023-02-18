# ENERGY PRICES

|Total & Raw|Transport & Tax|
|:---:|:---:|
|![Total ](./Images/Sk%C3%A6rmbillede%20fra%202023-02-18%2015-25-10.png)|![](./Images/Sk%C3%A6rmbillede%20fra%202023-02-18%2015-25-26.png)|

## Kilder:

* [Nordpool Integration](https://github.com/custom-components/nordpool)
  * Video Tutorial: [How to Track DYNAMIC ENERGY PRICES in Home Assistant NOW!](https://www.youtube.com/watch?v=NFJ510uhswY "Smart Home Junkie")
* [Apexcharts-card](https://github.com/RomRider/apexcharts-card)
  * [ApexCharts Tutorial: Advanced Graphs For Your Home Assistant UI](https://smarthomescene.com/guides/apexcharts-card-advanced-graphs-for-your-home-assistant-ui/)

## HACS

### Hent Nordpool integration & apexchart-card frontend

* HACS
  * Integrations - **Video timestamp 00:01:11**
    * EXPLORE & DOWNLOAD REPOSITORY
      * Search for: nordpool
        * Download nordpool
  * Frontend - **Video timestamp 00:10:00**
    * EXPLORE & DOWNLOAD REPOSITORY
      * Search for: apexchart-card
        * Download apexchart-card
  * Restart Home Assistant
    * Developer Tools
      * YAML
        * Check and Restart
          * CHECK CONFIGURATION
          * RESTART

### Install Nordpool Integration

* Settings - **Video timestamp 00:01:58**
  * Devices & Services
    * Integrations
      * ADD INTEGRATION: Nordpool
        * Region: DK1
        * Currency: DKK
        * Include VAT: Yes
        * Decimal rounding precision: 3
          * Low Price percentage: 1
          * Energy scale: kWh
          * NO additional cost

## Templates

### Add template file

* Add a template file to Home Assistant - **Video timestamp 00:06:21**
  * Filename: **/config/templates.yaml**
* Edit **/config/configurations.yaml** to include the template file
  * **template: !include templates.yaml**
* Restart Home Assistant
  * Developer Tools
    * YAML
      * Check and Restart
        * CHECK CONFIGURATION
        * RESTART

### Edit templates.yaml  - Video timestamp 00:07:14

File: **/config/templates.yaml**

```yaml
# How to Track DYNAMIC ENERGY PRICES in Home Assistant NOW!
#   Kilde: https://www.youtube.com/watch?v=NFJ510uhswY
#   templates.yaml # timestamp 7:14
# ---------------------------------------------------------  
- sensor:
    ##### Energy Prices  #####
    - name: "Energy Prices"
      unique_id: 02479b64-feff-4476-a96d-5c49e22a97ab
      icon: mdi:flash-alert
      unit_of_measurement: "DKK"
      state: >
        {{ states('sensor.nordpool_kwh_dk1_dkk_3_10_025')}}
      attributes:
        times: >
          {% set ns = namespace(times=[]) -%}
          {%- set today = state_attr('sensor.nordpool_kwh_dk1_dkk_3_10_025','raw_today') -%}
          {%- for hours in today -%}
            {%- set ns.times = ns.times + [as_local((hours.start)).strftime("%Y-%m-%d %H:%M:%S")] -%}
          {%- endfor -%}
          {%- set tomorrow = state_attr('sensor.nordpool_kwh_dk1_dkk_3_10_025','raw_tomorrow') -%}
          {%- for hours in tomorrow -%}
            {%- set ns.times = ns.times + [as_local((hours.start)).strftime("%Y-%m-%d %H:%M:%S")] -%}
          {%- endfor -%}
          {{ ns.times }}
        raw_prices: >
          {% set ns = namespace(raw_prices=[]) -%}
          {%- set today = state_attr('sensor.nordpool_kwh_dk1_dkk_3_10_025','raw_today') -%}
          {%- for hours in today -%}
            {%- set ns.raw_prices = ns.raw_prices + [hours.value] -%}
          {%- endfor -%}
          {%- set tomorrow = state_attr('sensor.nordpool_kwh_dk1_dkk_3_10_025','raw_tomorrow') -%}
          {%- for hours in tomorrow -%}
          {% if hours.value %}
            {%- set ns.raw_prices = ns.raw_prices + [hours.value] -%}
          {% endif %}  
          {%- endfor -%}
          {{ ns.raw_prices }}
        transport_prices: "{{ 0.1212, 0.1212, 0.1212, 0.1212, 0.1212, 0.1212, 0.3635, 0.3635, 0.3635, 0.3635, 0.3635, 0.3635, 
                              0.3635, 0.3635, 0.3635, 0.3635, 0.3635, 1.0905, 1.0905, 1.0905, 1.0905, 0.3635, 0.3635, 0.3635,
                              0.1212, 0.1212, 0.1212, 0.1212, 0.1212, 0.1212, 0.3635, 0.3635, 0.3635, 0.3635, 0.3635, 0.3635,
                              0.3635, 0.3635, 0.3635, 0.3635, 0.3635, 1.0905, 1.0905, 1.0905, 1.0905, 0.3635, 0.3635, 0.3635 }}"
        elafgift:         "{{ 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01,
                              0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01,
                              0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01 }}"
```

## Lovelace

### Create the Apexbar-Cart

```yaml
type: vertical-stack
cards:
  - type: horizontal-stack
    cards:
      - type: vertical-stack
        cards:
          - type: custom:simple-clock-card
            hide_seconds: true
            use_military: true
            font_size: 40px
            padding_size: 10px
      - type: vertical-stack
        cards:
          - type: horizontal-stack
            cards:
              - type: custom:button-card
                icon: mdi:home
                tap_action:
                  action: navigate
                  navigation_path: /lovelace/0
                styles:
                  card:
                    - height: 40px
              - type: custom:button-card
                icon: mdi:chevron-down
                tap_action:
                  action: navigate
                  navigation_path: /lovelace/more
                styles:
                  card:
                    - height: 40px
  - type: vertical-stack
    cards:
      - type: custom:apexcharts-card
        graph_span: 36h
        apex_config:
          chart:
            stacked: true
        header:
          title: Total Energi Price (DKK/kwh)
          show: true
        span:
          start: day
        now:
          show: true
          label: Now
        series:
          - entity: sensor.energy_prices
            name: Tax
            type: column
            color: yellow
            float_precision: 3
            data_generator: >-
              return entity.attributes.times.map((time, index) => {return [new
              Date(time).getTime(), entity.attributes.elafgift[index]] });
          - entity: sensor.energy_prices
            name: Transport Prices
            type: column
            color: blue
            float_precision: 3
            data_generator: >-
              return entity.attributes.times.map((time, index) => {return [new
              Date(time).getTime(), entity.attributes.transport_prices[index]]
              });
          - entity: sensor.energy_prices
            name: Raw Prices
            type: column
            color: red
            float_precision: 3
            data_generator: >-
              return entity.attributes.times.map((time, index) => {return [new
              Date(time).getTime(), entity.attributes.raw_prices[index]]});
        yaxis:
          - min: 0
            max: 3.5
            decimals: 3
            apex_config:
              tickAmount: 10
      - type: custom:apexcharts-card
        graph_span: 36h
        header:
          title: Raw Energi Price (DKK/kwh)
          show: true
        span:
          start: day
        now:
          show: true
          label: Now
        series:
          - entity: sensor.energy_prices
            color: red
            type: column
            float_precision: 3
            data_generator: >-
              return entity.attributes.times.map((time, index) => {return [new
              Date(time).getTime(), entity.attributes.raw_prices[index]] });
        yaxis:
          - min: 0
            max: 1.5
            decimals: 3
            apex_config:
              tickAmount: 10
      - type: custom:apexcharts-card
        graph_span: 36h
        header:
          title: Transport Energi Price (DKK/kwh)
          show: true
        span:
          start: day
        now:
          show: true
          label: Now
        series:
          - entity: sensor.energy_prices
            color: blue
            type: column
            float_precision: 3
            data_generator: >-
              return entity.attributes.times.map((time, index) => {return [new
              Date(time).getTime(), entity.attributes.transport_prices[index]]
              });
        yaxis:
          - min: 0
            max: 1.5
            decimals: 3
            apex_config:
              tickAmount: 10
      - type: custom:apexcharts-card
        graph_span: 36h
        header:
          title: Tax Energi Price (DKK/kwh)
          show: true
        span:
          start: day
        now:
          show: true
          label: Now
        series:
          - entity: sensor.energy_prices
            color: yellow
            type: column
            float_precision: 3
            data_generator: >-
              return entity.attributes.times.map((time, index) => {return [new
              Date(time).getTime(), entity.attributes.elafgift[index]] });
        yaxis:
          - min: 0
            max: 0.1
            decimals: 3
            apex_config:
              tickAmount: 10
```
