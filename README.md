# NextPath SmartStudy – IoT Module

Solução IoT desenvolvida para a Global Solution 2025/2 – FIAP  
**Tema:** O Futuro do Trabalho  
**Projeto:** NextPath – SkillUp AI  
**Aluno:** Gabriel Nakamura Ogata – RM560671  
Julio Cesar Dias Vilella rm560494
Guilherme Costeira Braganholo rm560628

---

##  Visão Geral

O NextPath SmartStudy IoT é um sistema criado para monitorar o ambiente de estudo do usuário, enviando dados em tempo real via MQTT para o Node-RED, onde são processados e exibidos em um dashboard.

Seu objetivo é melhorar foco, registrar automaticamente sessões de estudo e gerar alertas inteligentes sobre condições do ambiente.

Arquitetura da Solução

ESP32 (LDR) → MQTT (Broker Mosquitto) → Node-RED → Dashboard Web
Opcional: API Java para armazenamento de sessões de estudo.

Componentes utilizados:

ESP32 ou Wokwi

Sensor LDR

Broker MQTT: test.mosquitto.org

Node-RED

Node-RED Dashboard

Payload Enviado pelo ESP32

O dispositivo publica no tópico:

nextpath/estudo

Formato enviado:

{
"usuarioId": 1,
"estudando": true,
"ambienteBom": true,
"luminosidade": 350,
"timestamp_ms": 1732390200000
}

Processamento no Node-RED

O arquivo flows.json contém:

Recebimento de mensagens MQTT

Conversão de JSON

Cálculo do tempo de estudo

Verificação do ambiente (bom ou ruim)

Emissão de alerta quando a luz está baixa

Envio de dados para o dashboard

Métricas calculadas:

Tempo real de estudo no dia

Status “Estudando Agora”

Última luminosidade recebida

Texto de notificação quando necessário

Dashboard

O dashboard exibe:

Estudando Agora (true/false)

Tempo acumulado de estudo em segundos (gauge)

Gráfico de luminosidade das últimas leituras

Alerta de luz baixa (texto)

Acesse o dashboard pelo navegador:

http://localhost:1880/ui

Orientações para Configuração, Execução e Testes
1. Executar o Node-RED

No terminal, iniciar o Node-RED:

node-red

Acessar no navegador:

http://localhost:1880

Importar o fluxo:

Menu → Import → Upload → flows.json → Deploy

2. Configurar o ESP32 no Wokwi

Acessar:

https://wokwi.com

Criar um projeto com ESP32.

Adicionar o código do projeto (fornecido na pasta esp32).

Requisitos do código:

WiFi configurado como Wokwi-GUEST

MQTT apontando para test.mosquitto.org

Leitura do sensor LDR

Publicação no tópico nextpath/estudo

Envio contínuo a cada 2 segundos

Iniciar a simulação.

A luminosidade pode ser alterada movendo o LDR no editor.

3. Testar o Dashboard

Acessar no navegador:

http://localhost:1880/ui

Testes recomendados:

Teste de luminosidade

Ambiente com mais luz → Dashboard exibe ambiente bom

Ambiente escuro → Aparece alerta de luz baixa

Teste de sessão de estudo

Se o envio incluir estudando = true e ambienteBom = true, o tempo de estudo começa a subir automaticamente.

Teste do gráfico

O gráfico de luminosidade deve exibir os valores enviados pelo ESP32.

