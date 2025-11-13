# Análise de Requisitos - Plataforma IoT 2025

## ✅ O QUE JÁ ESTÁ IMPLEMENTADO

### 1. Dispositivos e Sensores ✅
- ✅ Suporte a múltiplos dispositivos ESP32
- ✅ Sistema modular de sensores/atuadores
- ✅ Sensores suportados:
  - ✅ DS18B20 (Temperatura)
  - ✅ DHT11 (Temperatura/Umidade)
  - ✅ MPU6050 (Acelerômetro/Giroscópio)
  - ✅ APDS9960 (Gestos e Cor)
  - ✅ HCSR04 (Ultrassônico)
  - ✅ KY-023 (Joystick)
  - ✅ Keypad 4x4 (Teclado Matricial)
  - ✅ IR Receiver (Controle Remoto)
  - ✅ Encoder
  - ✅ Botão
  - ✅ Relé
  - ✅ Motor de Vibração

### 2. Comunicação e Transmissão ✅
- ✅ MQTT seguro (TLS) como protocolo de comunicação
- ✅ Broker MQTT configurável (EMQX)
- ✅ Tópicos estruturados: `grupoX/sensor/{tipo}/{base}/position`
- ✅ Tópicos de atuadores: `grupoX/atuador/{tipo}/{pino}`
- ✅ Configuração via MQTT: `grupoX/config`
- ✅ Wi-Fi Manager para configuração de rede

### 3. Ingestão, Armazenamento e Processamento ✅
- ✅ Ingestão via MQTT
- ✅ Armazenamento MongoDB
- ✅ Modelos de dados (Device, Reading, Rule)
- ✅ Filtro de dados duplicados (buffer de últimas leituras)
- ✅ Validação de dados antes de salvar
- ⚠️ **FALTA**: Pré-processamento avançado (filtros, agregações, análises básicas)

### 4. Aplicação / Visualização ✅
- ✅ Interface web moderna (React + TypeScript)
- ✅ Dashboard com gráficos em tempo real
- ✅ Visualização de dispositivos e status online/offline
- ✅ Gráficos temporais (Recharts)
- ✅ Sistema de alertas (frontend)
- ✅ Histórico de eventos
- ✅ Relatórios (CSV, PDF, DOCX)
- ✅ Data Visualization com comparação entre dispositivos
- ✅ Sistema de automação (regras)
- ✅ API REST documentada (Swagger)

### 5. Deploy e Testes ⚠️
- ✅ Código organizado em repositório
- ⚠️ **FALTA**: Scripts de instalação
- ⚠️ **FALTA**: Docker/Docker Compose
- ⚠️ **FALTA**: Documentação completa de deploy
- ⚠️ **FALTA**: Manual de utilização completo

---

## ❌ O QUE FALTA IMPLEMENTAR

### 1. Rotas de API Faltantes 🔴

#### GET /api/devices
**Status**: ❌ FALTA
**Uso**: Frontend tenta usar em `Devices.tsx` linha 81
**Impacto**: Não é possível listar dispositivos no frontend

#### PUT /api/device/:espId
**Status**: ❌ FALTA
**Uso**: Frontend tenta usar em `Devices.tsx` linha 178
**Impacto**: Não é possível editar dispositivos

#### DELETE /api/device/:espId
**Status**: ❌ FALTA
**Uso**: Frontend tenta usar em `Devices.tsx` linha 230
**Impacto**: Não é possível deletar dispositivos

### 2. Suporte a LEDs 🔴

#### LEDs RGB ou individuais (Verde, Amarelo, Vermelho)
**Status**: ❌ FALTA
**Requisito**: ESP4 precisa controlar 3 LEDs (verde, amarelo, vermelho)
**Impacto**: Não é possível implementar o setup de teste final
**Necessário**:
- Classe `LedAtuador` no firmware
- Suporte no `SensorManager`
- Rotas de API para controlar LEDs
- Interface no frontend

### 3. Sistema de Controle de Acesso 🔴

#### Autenticação por senha (Teclado Matricial)
**Status**: ⚠️ PARCIAL
**O que existe**: Sensor de teclado matricial funciona
**O que falta**:
- Lógica de validação de senha (*1234)
- Comunicação entre ESPs para autorizar acesso
- Integração com motor de vibração (feedback tátil)
- Integração com LEDs (feedback visual)
- Integração com relé (desbloqueio de porta)

#### Monitoramento de Porta (Encoder)
**Status**: ⚠️ PARCIAL
**O que existe**: Sensor encoder funciona
**O que falta**:
- Lógica de detecção de porta aberta/fechada
- Timer para alerta de porta aberta (>5s)
- Integração com LEDs para alerta
- Integração entre ESP2 e ESP4

#### Monitoramento Ambiental com Alertas
**Status**: ⚠️ PARCIAL
**O que existe**: Sensor DHT11 funciona
**O que falta**:
- Lógica de limite de temperatura
- Integração com LEDs (amarelo = alerta)
- Notificações quando temperatura excede limite

### 4. Comunicação entre ESPs 🔴

#### Sistema de Coordenação
**Status**: ❌ FALTA
**Requisito**: ESPs precisam se comunicar entre si via MQTT
**Exemplo**:
- ESP1 (Teclado) → Valida senha → Publica no MQTT
- Backend recebe → Valida → Publica comando para ESP2 (Relé) e ESP4 (LEDs)
- ESP2 (Relé) → Recebe comando → Desbloqueia porta
- ESP4 (LEDs) → Recebe comando → Acende LED verde/vermelho

**Necessário**:
- Tópicos MQTT para comunicação entre ESPs
- Lógica no backend para orquestrar ações
- Handlers nos ESPs para receber comandos

### 5. Pré-processamento de Dados ⚠️

#### Filtros e Agregações
**Status**: ⚠️ PARCIAL
**O que existe**: Filtro básico de duplicatas
**O que falta**:
- Filtros de outliers
- Agregações em tempo real (média móvel, etc.)
- Análises básicas (tendências, padrões)
- Pré-processamento antes de armazenar

### 6. Documentação e Deploy 🔴

#### Scripts de Instalação
**Status**: ❌ FALTA
**Necessário**:
- Script de instalação do backend (npm install, configuração de variáveis)
- Script de instalação do frontend
- Script de configuração do MongoDB
- Script de configuração do MQTT

#### Docker/Docker Compose
**Status**: ❌ FALTA
**Necessário**:
- Dockerfile para backend
- Dockerfile para frontend
- docker-compose.yml com todos os serviços
- Documentação de uso

#### Manual de Utilização
**Status**: ⚠️ PARCIAL
**O que existe**: README básico
**O que falta**:
- Manual completo de instalação
- Manual de configuração de dispositivos
- Manual de uso da plataforma
- Guia de troubleshooting

#### Relatório Técnico
**Status**: ❌ FALTA
**Necessário**:
- Descrição da arquitetura
- Justificativas das escolhas tecnológicas
- Diagramas de arquitetura
- Documentação de APIs

### 7. Funcionalidades do Setup de Teste Final 🔴

#### ESP1 - Teclado Matricial + Motor Vibração
**Status**: ⚠️ PARCIAL
- ✅ Teclado funciona
- ✅ Motor de vibração existe
- ❌ Lógica de validação de senha
- ❌ Integração entre teclado e motor
- ❌ Feedback tátil (curto/longo)

#### ESP2 - Relé + Encoder
**Status**: ⚠️ PARCIAL
- ✅ Relé funciona
- ✅ Encoder funciona
- ❌ Lógica de detecção de porta
- ❌ Timer de alerta (5s)
- ❌ Integração entre relé e encoder

#### ESP3 - DHT11
**Status**: ✅ COMPLETO
- ✅ Sensor funciona
- ✅ Leituras periódicas
- ⚠️ FALTA: Integração com alertas (LED amarelo)

#### ESP4 - 3 LEDs
**Status**: ❌ FALTA
- ❌ Classe para controlar LEDs
- ❌ Suporte no firmware
- ❌ Integração com outros ESPs
- ❌ Lógica de estados (verde/vermelho/amarelo)

---

## 📋 PRIORIDADES DE IMPLEMENTAÇÃO

### Prioridade ALTA (Crítico para apresentação)
1. **Rotas de API faltantes** (GET/PUT/DELETE /api/devices)
2. **Suporte a LEDs** (ESP4)
3. **Sistema de controle de acesso** (validação de senha)
4. **Comunicação entre ESPs** (orquestração via MQTT)
5. **Documentação básica** (manual de instalação e uso)

### Prioridade MÉDIA (Importante para completude)
6. **Pré-processamento de dados** (filtros, agregações)
7. **Docker/Docker Compose** (facilitar deploy)
8. **Relatório técnico** (documentação completa)

### Prioridade BAIXA (Melhorias)
9. **Testes automatizados**
10. **Monitoramento e logging avançado**

---

## 🔧 RECOMENDAÇÕES TÉCNICAS

### 1. Implementar Rotas de API
Criar arquivo `iot2025back/src/routes/devices.js` com:
- GET /api/devices - Listar todos os dispositivos
- GET /api/device/:espId - Obter dispositivo específico
- PUT /api/device/:espId - Atualizar dispositivo
- DELETE /api/device/:espId - Deletar dispositivo

### 2. Implementar Suporte a LEDs
Criar classe `LedAtuador` similar a `ReleAtuador`:
- Suporte a múltiplos LEDs (RGB ou individuais)
- Comandos: ON/OFF, RGB values
- Tópicos MQTT: `grupoX/atuador/led/{pino}`

### 3. Implementar Sistema de Controle de Acesso
Criar serviço no backend (`iot2025back/src/services/accessControl.js`):
- Validação de senha
- Orquestração de ações (relé, LEDs, motor)
- Gerenciamento de estados

### 4. Implementar Comunicação entre ESPs
Usar tópicos MQTT específicos:
- `grupoX/access/request` - Solicitação de acesso
- `grupoX/access/response` - Resposta de acesso
- `grupoX/access/authorized` - Acesso autorizado
- `grupoX/access/denied` - Acesso negado

### 5. Implementar Docker
Criar Dockerfiles e docker-compose.yml para:
- Backend (Node.js)
- Frontend (React)
- MongoDB (opcional, pode usar Atlas)
- MQTT Broker (opcional, pode usar cloud)

---

## 📊 RESUMO EXECUTIVO

### Status Geral: ⚠️ 70% Completo

**O que funciona bem:**
- ✅ Infraestrutura básica (MQTT, MongoDB, Frontend)
- ✅ Sensores individuais funcionam
- ✅ Visualização de dados
- ✅ Sistema de regras básico

**O que precisa ser feito:**
- 🔴 Rotas de API faltantes (crítico)
- 🔴 Suporte a LEDs (crítico para teste)
- 🔴 Sistema de controle de acesso (crítico para teste)
- 🔴 Documentação e deploy (importante)

**Estimativa de tempo para completar:**
- Rotas de API: 2-3 horas
- Suporte a LEDs: 4-6 horas
- Sistema de controle de acesso: 8-12 horas
- Documentação e deploy: 4-6 horas
- **Total: 18-27 horas de desenvolvimento**

---

## 🎯 CONCLUSÃO

O projeto está **bem estruturado** e com **boa base técnica**, mas falta implementar funcionalidades **críticas** para o setup de teste final, especialmente:
1. Comunicação entre ESPs
2. Sistema de controle de acesso
3. Suporte a LEDs
4. Rotas de API faltantes

Com essas implementações, o projeto estará pronto para a apresentação.

