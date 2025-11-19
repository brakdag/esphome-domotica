# 1. Controlador de Termotanque

Este firmware controla el encendido y apagado del termotanque, para usar excedentes de producción fotovoltaica con inyección cero.

## 2. Hardware y Diagrama de Pines

* **Controlador:** ESP01s
* **Relé:** ESP01s 5V (activado por el Pin GPIO0)
* **Medidor de energía:** Shelly EM gen3.

## 3. Firmware (ESPHome)

El firmware para el ESP-01 se encuentra en el siguiente archivo:
* [`esphome/termotanque.yaml`](./esphome/termotanque.yaml)

## 4. Configuración en Home Assistant

Par a integrar este dispositivo en Home Assistant, se utilizan las siguientes automatizaciones y scripts.

### Automatización: Calentamiento Inteligente

Esta automatización de zondeo.

```yaml
  alias: Ejecutar Gestor de Termo (Sondeo)
  description: Ejecuta el script de sondeo del termo cada 10 minutos
  triggers:
  - minutes: /10
    trigger: time_pattern
  conditions:
  - condition: state
    entity_id: sun.sun
    state: above_horizon
  actions:
  - action: script.script_gestor_termo_v2_sondeo_2
    data: {}
  mode: single
```

### Script de zondeo de potencia.

```yaml

alias: Script Gestor Termo v2(Sondeo)
  description: Sondea si el sistema puede manejar el termotanque (350W) sin importar
    de la red.
  mode: restart
  variables:
    switch_id: switch.esp01_relay_termotaque
    sensor_red: sensor.shellyemg3_b08184e83968_energy_meter_0_power
    umbral_import_apagado: 100
    tiempo_espera_sondeo: 45
  sequence:
  - choose:
    - conditions:
      - condition: template
        value_template: '{{ is_state(switch_id, ''on'') }}'
      sequence:
      - variables:
          p_red_actual: '{{ states(sensor_red) | float(0) }}'
      - condition: template
        value_template: '{{ p_red_actual > umbral_import_apagado }}'
      - target:
          entity_id: '{{ switch_id }}'
        action: switch.turn_off
    - conditions:
      - condition: template
        value_template: '{{ is_state(switch_id, ''off'') }}'
      sequence:
      - target:
          entity_id: '{{ switch_id }}'
        action: switch.turn_on
      - delay:
          seconds: 45
      - variables:
          p_red_despues_del_sondeo: '{{ states(sensor_red) | float(0) }}'
      - condition: template
        value_template: '{{ p_red_despues_del_sondeo > umbral_import_apagado }}'
      - target:
          entity_id: '{{ switch_id }}'
        action: switch.turn_off
    default: []
```
