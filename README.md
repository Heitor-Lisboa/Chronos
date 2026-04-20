# Chronos

Sistema de monitoramento e automação para data center baseado em dispositivos embarcados (ESP32/ESP8266) integrados ao Home Assistant.

O sistema realiza a coleta contínua de dados ambientais (temperatura, umidade, luminosidade e presença de gás) e automatiza o controle de ar-condicionado para manter condições ideais de operação.

Projeto desenvolvido no IFRN – Campus São Gonçalo do Amarante.


## Objetivo

Monitorar variáveis críticas do ambiente e automatizar respostas a condições adversas, como aumento de temperatura ou detecção de gás.


## Arquitetura do Sistema

Fluxo de funcionamento:

```
Sensores → ESP32/ESP8266 → Rede Wi-Fi → Home Assistant → Controle de Ar-Condicionado
```

Os sensores coletam dados ambientais, que são enviados pelos microcontroladores para o Home Assistant via rede, onde são processados e utilizados em automações.


## Sensores Utilizados

- **Temperatura e Umidade:** AHT10 / AHT20 (I2C)  
- **Luminosidade:** Sensor de Luminosidade LDR HW-072   
- **Gás/Fumaça:** sensor MQ-2 (saída digital)  

## Funcionamento

- Coleta contínua de dados ambientais  
- Transmissão dos dados via Wi-Fi  
- Monitoramento em tempo real  
- Execução de automações  
- Detecção de condições críticas  

---

## Configuração

As configurações específicas de cada sensor estão organizadas na pasta `/configs`.

Abaixo está um exemplo simplificado de configuração completa:

```yaml
# Configuração geral (exemplo demonstrativo)

i2c:
  sda: 21
  scl: 22
  scan: true
  id: bus_a

sensor:
  - platform: aht10
    variant: AHT20
    temperature:
      name: "Temperatura"
    humidity:
      name: "Umidade"

binary_sensor:
  - platform: gpio
    pin: GPIO14
    name: "Luz Ambiente"

  - platform: gpio
    pin: GPIO27
    name: "Alarme de Gás"

# Wi-Fi e integração com Home Assistant omitidos por confidencialidade institucional
```

---

## Confidencialidade

Parte da configuração original foi omitida por conter credenciais e informações institucionais.

O exemplo apresentado representa apenas a estrutura geral do sistema.


## Autores

- **Heitor Lisboa dos Santos**  
  Estudante de Informática – IFRN  

- **Fábio Franco**  
  Professor Orientador de projeto – IFRN
