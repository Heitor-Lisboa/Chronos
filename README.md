# Chronos

Sistema de monitoramento e automação para data center baseado em dispositivos embarcados (ESP32/ESP8266) integrados ao Home Assistant.

O sistema realiza a coleta contínua de dados ambientais (temperatura, umidade, luminosidade e presença de gás) e automatiza o controle de ar-condicionado para manter condições ideais de operação.

Projeto desenvolvido no IFRN – Campus São Gonçalo do Amarante.

---

## Objetivo

Monitorar variáveis críticas do ambiente e automatizar respostas a condições adversas, como aumento de temperatura ou detecção de gás.

---

## Arquitetura do Sistema

Fluxo de funcionamento:

Sensores → ESP32/ESP8266 → Rede Wi-Fi → Home Assistant → Controle de Ar-Condicionado


Os sensores coletam dados ambientais, que são enviados pelos microcontroladores para o Home Assistant via rede, onde são processados e utilizados em automações.

---

## Sensores Utilizados

- **Temperatura e Umidade:** AHT10 / AHT20 (I2C)  
- **Luminosidade:** sensor digital via GPIO  
- **Gás/Fumaça:** sensor MQ-2 (saída digital)  

---

## Funcionamento

- Coleta contínua de dados ambientais  
- Transmissão dos dados via Wi-Fi  
- Monitoramento em tempo real  
- Execução de automações  
- Detecção de condições críticas  

---

## Configuração (ESPHome)

```yaml
i2c:
  sda: 21
  scl: 22
  scan: true
  id: bus_a
  frequency: 100kHz

sensor:
  - platform: aht10
    variant: AHT20
    i2c_id: bus_a
    address: 0x38
    temperature:
      name: "Temperatura"
    humidity:
      name: "Umidade"
    update_interval: 20s

binary_sensor:
  - platform: gpio
    pin:
      number: GPIO14
      mode: INPUT_PULLUP
      inverted: true
    name: "Luz Ambiente"
    device_class: light

  - platform: gpio
    pin:
      number: GPIO27
      mode: INPUT_PULLUP
      inverted: true
    name: "Alarme de Gás"
    device_class: gas
