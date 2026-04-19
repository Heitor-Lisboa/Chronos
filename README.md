# Chronos

Sistema de monitoramento e automação para data center baseado em dispositivos embarcados (ESP32/ESP8266) integrados ao Home Assistant.

O projeto realiza a coleta contínua de dados ambientais (temperatura, umidade, luminosidade e presença de gás) e utiliza essas informações para automatizar o controle de ar-condicionado, mantendo condições ideais de operação no ambiente.

Projeto desenvolvido no IFRN – Campus São Gonçalo do Amarante.

---

## Objetivo

Monitorar variáveis críticas do data center em tempo real e automatizar respostas a condições adversas, como aumento de temperatura ou detecção de gás.

---

## Arquitetura do Sistema

O sistema é composto por sensores conectados a microcontroladores ESP32, responsáveis por coletar e transmitir os dados para o Home Assistant, onde são processados e utilizados em automações.

Sensores → ESP32/ESP8266 → Rede Wi-Fi → Home Assistant → Controle de Ar-Condicionado

---

## Sensores Utilizados

- **Temperatura e Umidade:** AHT10 / AHT20 (via I2C)  
- **Luminosidade:** sensor digital (GPIO)  
- **Gás/Fumaça:** sensor MQ-2 (saída digital)  

---

## Funcionamento

- Coleta contínua de dados ambientais  
- Envio dos dados via rede para o Home Assistant  
- Monitoramento em tempo real  
- Execução de regras de automação (ex: controle de temperatura)  
- Detecção de eventos críticos (ex: presença de gás)  

---

## Exemplo de Configuração (ESPHome)

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

  - platform: gpio
    pin:
      number: GPIO27
      mode: INPUT_PULLUP
      inverted: true
    name: "Alarme de Gás"
