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
