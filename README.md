# Painel de Controle de Umidificadores (IoT)

Painel web para monitorar e controlar umidificadores à distância, com comunicação em tempo real via **MQTT**.

O painel mostra a umidade e o status de cada dispositivo e permite ajustar os parâmetros de funcionamento sem acesso físico ao equipamento.

## Funcionalidades

- **Login** para acessar o painel
- **Visão geral** dos dispositivos conectados, com umidade atual e status
- **Tela de detalhes** de cada umidificador, com os limites configurados no momento
- **Configuração remota** de:
  - umidade mínima e máxima
  - tempo máximo ligado (em minutos)
- **Validação** dos valores antes do envio (ex.: mínima menor que máxima)
- **Ativar / desativar** o sistema de cada dispositivo
- Suporte a dois dispositivos, sendo um deles controlado por **potenciômetro**

## Tecnologias

- HTML, CSS e JavaScript (sem frameworks)
- [MQTT.js](https://github.com/mqttjs/MQTT.js) via WebSocket seguro (`wss`)
- Broker MQTT público HiveMQ
- Dispositivos (microcontroladores) publicando leituras e assinando os comandos do painel

## Como funciona

```
[Umidificador / sensor]  <--MQTT-->  [Broker HiveMQ]  <--MQTT over WebSocket-->  [Painel web]
```

1. Cada dispositivo publica a umidade e o status em um tópico próprio.
2. O painel assina esses tópicos e atualiza a tela em tempo real.
3. Quando o usuário altera um parâmetro, o painel publica a nova configuração e o dispositivo aplica os valores.

## Como executar

Por ser uma página estática, basta abrir o `index.html` no navegador ou publicá-lo em qualquer hospedagem estática (GitHub Pages, Vercel, Netlify).

## Próximos passos

- Mover a autenticação para um backend (hoje a verificação é feita no navegador)
- Usar um broker privado com usuário e senha
- Guardar o histórico de umidade e exibir gráficos
