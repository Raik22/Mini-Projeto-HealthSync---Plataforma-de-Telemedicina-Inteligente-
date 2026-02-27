# 04 – Componentes e Módulos

## 4.1 Visão Geral dos Módulos

O sistema é composto pelos seguintes microsserviços (módulos):

| Módulo | Responsabilidade | Tecnologia Sugerida |
|--------|-----------------|---------------------|
| **auth-service** | Autenticação e autorização de usuários | Node.js / Spring Boot |
| **user-service** | Cadastro e perfil de pacientes e médicos | Node.js / Spring Boot |
| **appointment-service** | Agendamento e gestão de consultas | Node.js / Django |
| **video-service** | Sessões de videochamada | WebRTC / Twilio / Agora |
| **ehr-service** | Prontuário Eletrônico do Paciente (EHR) | Python / Spring Boot |
| **prescription-service** | Prescrição digital de medicamentos | Node.js / Spring Boot |
| **iot-service** | Recebimento e processamento de dados IoT | Python / Go |
| **notification-service** | Envio de e-mails, SMS e push notifications | Node.js / AWS SNS |
| **api-gateway** | Roteamento, autenticação e rate limiting | Kong / NGINX / AWS API Gateway |

---

## 4.2 Descrição Detalhada dos Módulos

### 4.2.1 auth-service

**Responsabilidade:** Gerenciar autenticação (login/logout), emissão de tokens JWT e refresh tokens.

**Interfaces:**
- `POST /auth/login` – autenticação de usuário.
- `POST /auth/refresh` – renovação do token de acesso.
- `POST /auth/logout` – invalidação do token.

**Dependências:** user-service (verificação de credenciais), Redis (blacklist de tokens).

---

### 4.2.2 user-service

**Responsabilidade:** CRUD de pacientes e médicos, verificação de CRM, upload de documentos.

**Interfaces:**
- `POST /users/patients` – cadastro de paciente.
- `POST /users/doctors` – cadastro de médico.
- `GET /users/{id}` – consulta de perfil.
- `PUT /users/{id}` – atualização de perfil.

**Dependências:** auth-service (autorização), banco de dados relacional (PostgreSQL).

---

### 4.2.3 appointment-service

**Responsabilidade:** Agendamento, cancelamento, listagem e histórico de consultas.

**Interfaces:**
- `POST /appointments` – agendar consulta.
- `GET /appointments/{id}` – detalhes da consulta.
- `PUT /appointments/{id}/cancel` – cancelar consulta.
- `GET /appointments/patient/{patientId}` – histórico do paciente.

**Dependências:** user-service, video-service, notification-service.

---

### 4.2.4 video-service

**Responsabilidade:** Criar e gerenciar sessões de videochamada entre paciente e médico.

**Interfaces:**
- `POST /video/sessions` – criar sessão de vídeo.
- `GET /video/sessions/{sessionId}/token` – obter token de acesso à sessão.

**Dependências:** appointment-service, provedores externos de vídeo (Twilio/Agora).

---

### 4.2.5 ehr-service (Prontuário Eletrônico)

**Responsabilidade:** Armazenar e recuperar o histórico clínico do paciente (consultas, diagnósticos, exames, alergias).

**Interfaces:**
- `POST /ehr/{patientId}/records` – adicionar registro clínico.
- `GET /ehr/{patientId}/records` – listar registros do paciente.
- `GET /ehr/{patientId}/records/{recordId}` – detalhe de um registro.

**Dependências:** user-service, MongoDB (armazenamento de documentos clínicos).

---

### 4.2.6 prescription-service

**Responsabilidade:** Emissão, assinatura digital e consulta de prescrições médicas.

**Interfaces:**
- `POST /prescriptions` – criar prescrição.
- `GET /prescriptions/{id}` – consultar prescrição.
- `GET /prescriptions/patient/{patientId}` – listar prescrições do paciente.

**Dependências:** user-service, ehr-service.

---

### 4.2.7 iot-service

**Responsabilidade:** Receber dados de dispositivos IoT/wearables (frequência cardíaca, pressão arterial, glicemia) e alertar médicos em casos anômalos.

**Interfaces:**
- Tópico MQTT `iot/devices/{deviceId}/data` – recebimento de telemetria.
- `GET /iot/patients/{patientId}/metrics` – consultar métricas do paciente.

**Dependências:** Kafka/MQTT broker, ehr-service, notification-service.

---

### 4.2.8 notification-service

**Responsabilidade:** Disparar notificações via e-mail, SMS e push notification (lembretes de consulta, alertas de saúde).

**Interfaces:**
- Consome eventos do message bus (agendamentos, alertas IoT).
- `POST /notifications/send` – envio manual de notificação.

**Dependências:** Kafka/RabbitMQ, provedores externos (SendGrid, Twilio SMS, Firebase FCM).

---

> **[TODO]** Adicione ou remova módulos conforme o escopo definido no seu projeto.

---

*[← 03 – Arquitetura do Sistema](03-arquitetura-sistema.md) | [05 – Modelo de Dados →](05-modelo-dados.md)*
