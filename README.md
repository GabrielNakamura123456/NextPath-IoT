# NextPath SmartStudy – IoT Module

Solução IoT desenvolvida para a Global Solution 2025/2 – FIAP  
**Tema:** O Futuro do Trabalho  
**Projeto:** NextPath – SkillUp AI  
**Aluno:** Gabriel Nakamura Ogata – RM560671  
Julio Cesar Dias Vilella rm560494
Guilherme Costeira Braganholo rm560628

---

##   Visão Geral

O **NextPath SmartStudy IoT** é um sistema IoT desenvolvido para monitorar o ambiente de estudo do usuário, enviando dados em tempo real para o Node-RED, onde são processados e exibidos em um dashboard completo.

O objetivo é melhorar o foco, registrar automaticamente sessões de estudo e fornecer alertas inteligentes usando IoT + MQTT + Node-RED.

Este módulo faz parte da plataforma global **NextPath – SkillUp AI**, focada em requalificação profissional e aprendizado contínuo.

---

##  Arquitetura da Solução

ESP32 (LDR) → MQTT (Mosquitto Broker) → Node-RED → Dashboard
↓
API Java (opcional)

markdown
Copiar código

### Componentes:
- **ESP32 ou Wokwi** – capta luminosidade
- **MQTT Broker** – test.mosquitto.org
- **Node-RED** – processamento e lógica
- **Dashboard Web** – visualização
- **Flows.json** – fluxo completo do projeto

---

##  Estrutura do Payload

O ESP32 envia dados no tópico:

nextpath/estudo

yaml
Copiar código

Formato:

```json
{
  "usuarioId": 1,
  "estudando": true,
  "ambienteBom": true,
  "luminosidade": 350,
  "timestamp_ms": 1732390200000
}




Processamento no Node-RED
O arquivo flows.json contém:

Recebimento MQTT

Parse de JSON

Cálculo de tempo de estudo

Controle de ambiente (bom/ruim)

Emissão de alerta automático

Atualização do Dashboard

Métricas calculadas:
Tempo real de estudo do dia

Status "Estudando Agora"

Luminosidade atual

Notificação caso a luz esteja baixa

 Dashboard
O dashboard exibe:

Estudando Agora (true/false)

Tempo acumulado de estudo (gauge)

Gráfico de luminosidade

Alerta de luz baixa

Acesse via:

bash
Copiar código
http://localhost:1880/ui
⚙ ORIENTAÇÕES PARA CONFIGURAÇÃO, EXECUÇÃO E TESTES
 1. Requisitos
Instale:

Node.js

Node-RED

Navegador (Chrome/Edge)

Conta no Wokwi (para simular ESP32)

Broker MQTT: test.mosquitto.org:1883

 2. Executar o Node-RED
No terminal:

Copiar código
node-red
Acesse:

arduino
Copiar código
http://localhost:1880
Importe o arquivo:

 Menu → Import → Upload → flows.json → Deploy

 3. Configurar o ESP32 no Wokwi
Entre em:

https://wokwi.com

Use o código fornecido no projeto, incluindo:

WiFi → Wokwi-GUEST

MQTT → test.mosquitto.org

Leitura do sensor LDR

Publicação no tópico nextpath/estudo

Inicie a simulação.
A luminosidade pode ser alterada movendo o LDR.

 4. Testar o Dashboard
Abra:

bash
Copiar código
http://localhost:1880/ui
Teste:

✔ Teste de luminosidade
Muita luz → Ambiente OK

Pouca luz → Alerta: “Luz baixa — ajuste iluminação”

✔ Teste de sessão de estudo
Se estudando = true e ambienteBom = true
→ o tempo começa a subir automaticamente.

✔ Teste de gráfico
Valores de luminosidade devem aparecer como nova linha no chart.

